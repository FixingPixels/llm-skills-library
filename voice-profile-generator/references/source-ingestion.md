---
title: Source Ingestion
load_at: mode-a-step-1
summary: Meeting transcript providers (Granola, Fireflies, Otter, Fathom, Read.ai, tl;dv, Grain, Zoom, Meet, Teams) as primary sources; paste/file/folder fallback; per-provider incremental pulls keyed off last_synced; confirm name once and store it in the profile
---

# Source Ingestion

Handle step 1 of Mode A: gather source material, compute the inventory, and confirm the small amount of metadata needed before analysis begins.

The skill knows what a **transcript** is, not which app produced it. Any meeting transcription tool that exposes "list recent items" and "fetch by id" is a valid **transcript source provider**. Paste/file/folder ingestion is the documented **fallback** when no provider is available — and a useful supplement for polished writing samples no transcription tool will ever have (blog posts, newsletters, LinkedIn posts).

Per-provider adapter notes (tool names, dedup keys, quirks) live in [`transcript-providers.md`](transcript-providers.md). Load that file only when you need to wire a specific provider.

## Contents

1. [Meeting transcript providers (primary)](#1-meeting-transcript-providers-primary)
2. [Fallback / supplemental sources](#2-fallback--supplemental-sources)
3. [Folder ingestion](#3-folder-ingestion)
4. [Classifying each source](#4-classifying-each-source)
5. [Compute and report the inventory](#5-compute-and-report-the-inventory)
6. [Name and content types](#6-name-and-content-types)

---

## 1. Meeting transcript providers (primary)

A **transcript source provider** is anything that exposes two capabilities the skill needs:

| Capability | What the skill uses it for |
|---|---|
| `list_since(timestamp)` | Incremental "get latest" pulls; first-build window selection |
| `fetch(id)` | Retrieve the full transcript for an item the user kept after review |

Known providers (no preferred order):

- **Granola** — MCP connector
- **Fireflies.ai** — MCP server or REST/GraphQL API
- **Otter.ai** — API or `.txt`/`.docx` exports
- **Fathom** — API or per-meeting `.txt` exports
- **Read.ai** — API or transcript exports
- **tl;dv** — API or `.txt`/`.srt` exports
- **Grain** — API or shareable transcripts
- **Zoom** — Cloud Recording API for `.vtt` transcripts; or downloaded `.vtt`/`.txt`
- **Google Meet** — Gemini transcripts in Drive (via the Drive MCP); Docs/`.txt` exports
- **Microsoft Teams** — Graph API; `.docx` transcript exports

See [`transcript-providers.md`](transcript-providers.md) for detection signals, list/fetch tool names, and dedup keys per provider.

### Provider discovery (runtime)

1. Enumerate enabled MCP servers/connectors and any configured API tokens in the environment. Match against the known-provider list.
2. Also scan any folder the user has pointed at for provider-shaped exports (e.g. `.vtt` files for Zoom, a "Meet Recordings" folder for Google Meet exports). A folder of exports is a perfectly valid provider — see [§3 Folder ingestion](#3-folder-ingestion).
3. Build the set of **available providers** for this session. Report it to the user briefly: *"Detected: Granola, Fireflies, and a folder of Zoom `.vtt` exports."*
4. If the set is empty, jump to [§2](#2-fallback--supplemental-sources) and tell the user the skill is running in fallback mode.
5. If the user explicitly names a provider that is not available ("pull from Otter") tell them which providers you actually see and ask whether to proceed with those.

### First build (no profile yet)

1. Ask the user for the time window or count to pull (sensible default: last 90 days, or the most recent ~20 meetings per provider). Confirm before listing.
2. For each available provider, call its list-recent capability with that window. Merge the candidate lists for review.
3. Show the candidate set (provider, title, date, duration/word count if available) and let the user deselect anything irrelevant — internal HR calls, NDA'd customer conversations, etc.
4. Fetch the full text/transcript for each surviving item. Sort deterministically by date (oldest -> newest) so re-runs are reproducible.
5. Continue to [§5](#5-compute-and-report-the-inventory).

### Incremental update ("get the latest meeting notes")

1. Read `references/voice-profile.md`. The metadata header carries a per-provider `last_synced` map and the list of previously ingested source ids (see [`profile-format.md`](profile-format.md)).
2. For each available provider, query items with `date > last_synced[provider]`.
3. Dedupe against the profile's recorded `sources` — never re-ingest something already analyzed.
4. Show the candidate new set to the user and let them deselect items before fetching. Same review step as the first build.
5. Fetch the survivors. Continue to [§5](#5-compute-and-report-the-inventory) — the inventory report should clearly mark this as an incremental pull, show the delta per provider, and note any provider that yielded nothing this run.

If a provider's adapter exposes neither a list-by-date nor a "since" filter, list a recent window and filter client-side using each item's date.

### Provider access caveats

- Some providers require explicit user approval per call in some hosts. Batch fetches when possible and tell the user how many approvals to expect.
- If a fetch fails for a specific item (permission, missing transcript, etc.), record it in the inventory under "Skipped" with the reason — never silently drop sources.
- A provider may go offline between runs (token expired, MCP disabled). Treat that as "this provider is unavailable for this run" and continue with whichever providers remain; do not modify the profile's `last_synced` map for unavailable providers.

---

## 2. Fallback / supplemental sources

Used when no transcript provider is available, or alongside one or more providers to add written craft samples (blog posts, newsletters, LinkedIn posts) that no transcription tool will see.

| Source type | How to ingest |
|-------------|---------------|
| Pasted text in chat | Use directly — no tool call needed |
| `.txt` or `.md` files | Read tool |
| `.docx` files | Bash + `python-docx` (`python -c "from docx import Document; print('\n'.join(p.text for p in Document('file.docx').paragraphs))"`) |
| `.vtt` files (Zoom / Meet exports) | Read tool; strip WEBVTT header + cue timing (`HH:MM:SS.mmm --> HH:MM:SS.mmm`) lines before analysis |
| A folder path the user points at | See [§3 Folder ingestion](#3-folder-ingestion) |
| Pasted URLs to public posts | WebFetch when the host allows it; otherwise ask the user to paste the text |

When running in pure fallback mode (no providers), explicitly tell the user: *"No transcript providers detected — running in fallback mode. The profile will still be built, but the incremental 'get the latest meeting notes' update path won't work until at least one provider is enabled."*

---

## 3. Folder ingestion

When the user gives a folder path (e.g. "use the files in `~/voice-samples/`"):

1. Use Glob to enumerate supported files recursively: `**/*.{txt,md,docx,vtt}` under the given path.
2. Read each match using the per-extension method above (strip VTT cue timing for `.vtt`).
3. List any unsupported files (`.pdf`, `.rtf`, `.html`, audio, video, etc.) under a "Skipped" line in the inventory so the user can convert and re-run. Do not silently drop them.
4. Sort surviving sources deterministically (alphabetical by relative path) before analysis so re-runs are reproducible.

A folder of provider exports is itself a transcript provider — record those sources with the originating provider name (e.g. `provider: zoom`, `origin: file`) so dedup, changelog, and the per-provider `last_synced` still work.

---

## 4. Classifying each source

Treat each item as one of two categories:

- **Transcripts** — items from any meeting transcription provider (Granola, Fireflies, Otter, Zoom, Meet, Teams, etc.), or recordings/interviews. Reveal authentic rhythm, vocabulary under pressure, and unedited idea structure.
- **Written samples** — blog posts, emails, LinkedIn posts, newsletters, any intentional prose. Reveal craft choices: openings, closings, edited vocabulary.

Items from any transcript provider are transcripts by default.

For file-based sources, classify using these signals (in order):

1. **Folder name**: a parent directory matching `transcripts?`, `calls?`, `meetings?`, `recordings?`, `cloud[_-]?recordings?`, `zoom`, `meet`, `granola`, `fireflies`, `otter`, `fathom`, `read([._-]?ai)?`, `tldv`, `grain`, `teams`, `interviews?` (case-insensitive) -> transcript. A parent matching `posts?`, `blog`, `newsletter`, `emails?`, `writing`, `drafts?` -> written sample.
2. **Filename**: same keyword patterns applied to the filename itself. `.vtt` files are transcripts.
3. **Content shape**: speaker labels (`Chris:`, `[Speaker 1]`, `00:14:32`), VTT cue blocks, filler words ("um", "uh"), and lack of paragraph structure -> transcript. Headings, intentional paragraph breaks, polished sentences -> written sample.

If classification is ambiguous for any file, list those files explicitly in the inventory report and ask the user to confirm before running the analysis. Do not guess silently.

---

## 5. Compute and report the inventory

For each source, note its provider (or `file` / `pasted` / `url`), type, origin id (provider id, file path, or pasted label), and approximate word count. Tell the user the total before continuing. For incremental updates, also report the cumulative word count (this run + everything previously analyzed in the profile) and break the new sources down by provider.

- **High confidence threshold**: ~2,000 cumulative words across all sources.
- Below threshold: proceed if asked, but flag in advance which dimensions will be low-confidence (typically Dimensions 4 and the closing-style portion of 7 when only transcripts are available).

---

## 6. Name and content types

**On the first build**, confirm two facts before analysis:

1. **Name** — how should it appear in the profile? (first name, full name, or handle). Stored in the profile's metadata header and reused on every subsequent update — do not ask again.
2. **Content types** — what will this profile be used to write? Examples: LinkedIn posts, blog articles, email newsletters, X threads, sales emails. Optional. If supplied, stored in the metadata header and used to scope the profile's writing instructions.

**On every subsequent update**, read these from the existing profile's metadata header. Do not re-ask. If the user wants to change them, accept the change in-session and update the header.
