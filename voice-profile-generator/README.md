# Voice Profile Generator

A Claude Agent Skill that builds and maintains a **single living voice profile** sourced from any meeting transcription tool you use (Granola, Fireflies, Otter, Fathom, Read.ai, tl;dv, Grain, Zoom, Google Meet, Microsoft Teams) — plus any pasted, attached, or folder-based material — and drives writing sessions from it with a post-session feedback loop that keeps the profile sharp over time.

This repo is the authoring source. The runtime install lives at `~/.claude/skills/voice-profile-generator/`.

## What it does

The skill maintains one canonical file inside itself:

```
references/voice-profile.md
```

That file is the single source of truth. The skill builds it on first run, updates it in place from then on, reads it before every drafting session, and offers to update it after each session based on the feedback you gave.

There are two modes, picked from intent:

- **Mode A — Build or update the profile.** Discovers available meeting transcript providers at runtime (any MCP / API / folder-of-exports for a known tool), pulls source material, runs the seven-dimension voice analysis, and writes or merges into `references/voice-profile.md`. Every update is a merge plus a changelog entry — prior evidence is preserved unless directly contradicted.
- **Mode B — Writing session.** Reads the profile, drafts in voice, iterates with you while capturing every correction and editing choice, and ends with a **Post-Session Feedback Summary** asking whether to fold the new signals into the profile.

## Supported transcript providers

The skill knows what a transcript is, not which app produced it. Any tool that exposes "list recent items" + "fetch by id" qualifies. Out of the box it recognizes:

| Provider | Access |
|---|---|
| Granola | MCP connector |
| Fireflies.ai | MCP server or REST/GraphQL API |
| Otter.ai | API or `.txt` / `.docx` exports |
| Fathom | API or per-meeting `.txt` exports |
| Read.ai | API or transcript exports |
| tl;dv | API or `.txt` / `.srt` exports |
| Grain | API or shareable transcripts |
| Zoom | Cloud Recording API or downloaded `.vtt` files |
| Google Meet | Gemini transcripts in Drive (Drive MCP) or Docs/`.txt` exports |
| Microsoft Teams | Graph API or `.docx` transcript exports |

Adapter notes (detection signals, list/fetch capability names, dedup keys, quirks) live in [`references/transcript-providers.md`](references/transcript-providers.md). New providers can be added in a small section there — the rest of the skill is unchanged.

Multiple providers can run in the same session. The skill discovers all available ones at runtime, lets you deselect items across the combined list, and tracks a separate `last_synced` watermark per provider so an incremental update only re-fetches what's actually new from each.

## Triggers

Any of these activate the skill:

- "build my voice profile", "analyze my voice"
- "get the latest meeting notes", "sync my meeting transcripts", "refresh my voice profile"
- Tool-specific phrasings: "get the latest Granola notes", "pull from Fireflies", "sync my Otter transcripts", "import my Fathom calls", "pull my Zoom recordings", "sync my Meet transcripts", "use my Teams transcripts"
- "draft this in my voice", "write as me", "edit this to sound like me"
- Pasted transcripts from any meeting tool
- Uploaded `.txt` / `.md` / `.docx` / `.vtt` files (transcripts or writing samples)
- A folder path pointed at any combination of the above

It does **not** trigger for generic writing help with no voice intent, transcribing audio, or TTS / voice cloning.

## How to use it

### Install

The runtime copy lives at `~/.claude/skills/voice-profile-generator/`. Sync this repo into it — but **never delete `references/voice-profile.md`**, that's your living profile.

```bash
# From this repo
mkdir -p ~/.claude/skills/voice-profile-generator
rsync -a --delete \
  --exclude='references/voice-profile.md' \
  SKILL.md references evals learnings.md \
  ~/.claude/skills/voice-profile-generator/
```

The `--exclude='references/voice-profile.md'` flag is critical. Without it, every reinstall wipes your profile.

If you skip `--delete` you don't need the exclude, but you'll accumulate stale files over time when references are renamed.

### Run

In any Claude session with skills enabled:

**First build (any provider):**

> "Build my voice profile from my Granola notes."

or

> "Build my voice profile from Fireflies."

or

> "Build my voice profile." (the skill picks up whichever providers are available)

The skill detects available providers, asks which time window or count to pull, lets you review and deselect candidate meetings, fetches the survivors, asks for your name (stored in the profile and never re-asked), optionally asks what content types you write for, runs the seven-dimension analysis, and writes `references/voice-profile.md` from scratch.

**First build (no providers):**

> "Build my voice profile from these blog posts." [paste / attach]

If no transcript provider is detected, the skill runs in fallback mode using pasted text, attached files, or a folder path you point at. It'll tell you it's in fallback mode so you can wire a provider later for the incremental update path.

**Incremental update (any or all providers):**

> "Get the latest meeting notes and update my voice profile."

The skill reads the per-provider `last_synced` map from the existing profile, pulls only newer items from each available provider, dedupes against prior sources, lets you deselect anything irrelevant, analyzes only the new material, merges into existing dimensions, and prepends a changelog entry to the Profile Update Log naming the providers, the per-provider source counts, and which watermarks moved.

**Multi-provider in one shot:**

> "Sync my Granola notes and pull anything new from Zoom into my voice profile."

Same flow, with provider-shaped breakdowns in the candidate review and the changelog.

**Writing session:**

> "Draft a LinkedIn post about pricing transparency in my voice."

The skill reads the profile, drafts, iterates with you, then closes with a Post-Session Feedback Summary mapping your edits to specific profile dimensions and asking whether to update the profile with them. Say "yes" and the change goes straight into the file with a changelog entry. Say "no" and nothing changes.

You can also update the profile **mid-session** without waiting for the summary:

> "Add 'in essence' to my avoid list — I'd never say that."

The skill applies the edit immediately, appends a changelog entry, and continues the writing session honoring the new rule.

### Folder layout (file-based providers and fallback)

If you'd rather hand it a folder of exported transcripts, this layout classifies cleanly:

```
~/voice-samples/
├── cloud-recordings/         # Zoom .vtt exports
│   ├── 2025-09-team-sync.vtt
│   └── 2025-09-customer-call.vtt
├── granola/                  # Granola exports
│   └── 2025-09-podcast.md
├── meet/                     # Google Meet transcript exports
│   └── 2025-09-design-review.txt
└── writing/                  # Polished prose (always supplemental)
    ├── blog/
    │   └── post-about-pricing.md
    └── newsletter/
        └── issue-12.md
```

A flat folder also works — the skill uses filename keywords and content shape (speaker labels, VTT cues, filler words) to classify each file and infer the originating provider.

### Recommended source volume

| Cumulative source words | Confidence |
|--------------|------------|
| ~2,000+ | High — all dimensions usable |
| 1,000–2,000 | Medium — some structural dimensions may be flagged |
| Under 1,000 | Low — skill will proceed if asked, but will flag low-confidence dimensions explicitly |

You hit the confidence threshold **cumulatively**, not per run. Three meeting syncs of 800 words each will lift you out of low-confidence territory just as well as one big initial build — that's the point of incremental updates.

## Repository layout

```
voice-profile-generator/
├── SKILL.md                          # Tier-2 routing document (two modes)
├── README.md                         # This file
├── references/
│   ├── source-ingestion.md           # Mode A step 1 — provider discovery + paste/file/folder fallback
│   ├── transcript-providers.md       # Per-provider adapter notes (loaded on demand)
│   ├── analysis-framework.md         # Mode A step 2 — seven dimensions + incremental-update note
│   ├── profile-format.md             # Mode A step 3 — living profile structure, merge rules, quality gate
│   ├── writing-session.md            # Mode B — draft, feedback summary, in-place updates
│   └── voice-profile.md              # The living profile (created by the skill, not committed)
├── evals/
│   └── evals.json                    # Realistic test prompts covering both modes and multiple providers
└── learnings.md                      # Self-improvement notes (pruned weekly)
```

The skill follows progressive disclosure from Anthropic's [skill authoring best practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices):

- **Tier 1** — YAML frontmatter in `SKILL.md` is always loaded (~150 tokens).
- **Tier 2** — `SKILL.md` body loads when the skill activates.
- **Tier 3** — Reference files load one at a time, only at the step that needs them. `transcript-providers.md` loads only when wiring a specific provider.

`references/voice-profile.md` is not a reference file in that sense — it's the user-state artifact the skill maintains. It's loaded explicitly at the start of every writing session and at the start of every update.

## Outputs

There is only one output: `references/voice-profile.md`. It contains:

- A YAML metadata header (name, per-provider `last_synced` map, sources list with `origin`/`provider`/`id`, cumulative word count, per-dimension confidence flags).
- The voice profile body — Voice Signature, Sentence Structure & Rhythm, Vocabulary (reach-for and avoid), Openings, Argument Architecture, Closings, Rhetorical Moves, What This Voice Is NOT, Signature Examples, Writing Instructions with a self-review checklist, and (optional) Content Type Notes.
- A Profile Update Log — a changelog with one entry per update (Provider sync, Manual sources, or In-session update).

No portable prompt file. No zipped `.skill`. If you want to use the profile in a different LLM, copy the body of `references/voice-profile.md` and paste it as a system prompt.

## Improving fidelity over time

You don't run "the whole thing again." You sync more meeting material from whichever provider(s) you use, accept profile updates from writing sessions, and watch low-confidence dimensions firm up. The changelog records what changed and when, so you can roll back manually if a sync drifted the profile in a direction you didn't want.

## Adding a new provider

If your meeting tool isn't in the list:

1. Open [`references/transcript-providers.md`](references/transcript-providers.md) and add a short section in the same shape as the others (Detection / List / Fetch / Dedup key / Notes).
2. If the tool offers exports to a folder, you don't even need that — point the skill at the folder and it'll auto-classify (use a parent folder name matching the tool, like `~/my-tool-exports/`).
3. Re-run `evals/evals.json` to sanity-check the change didn't break existing flows.

## Tests

Ten realistic test prompts live in [`evals/evals.json`](evals/evals.json), covering:

1. First build from Granola.
2. Generic-phrasing incremental update across all available providers.
3. First build from Fireflies (non-Granola provider path).
4. Multi-provider incremental update (Granola + Zoom).
5. User names an unavailable provider.
6. Mode B writing-session entry — read profile, draft, run checklist.
7. Post-Session Feedback Summary + update-the-profile offer.
8. Mid-session profile update applied immediately.
9. First build from a folder of Zoom `.vtt` exports.
10. Fallback build with no providers available.

Run them as a regression check after editing any reference file.

## Authoring conventions

This skill is built per the [skill-architect](file:///Users/ccollett/.claude/skills/skill-architect/) golden rules:

- `SKILL.md` body under 200 lines
- YAML description has Triggers / Does NOT trigger / Produces parts
- All references linked one level deep with explicit `references/...` paths
- Each reference has its own frontmatter (`title`, `load_at`, `summary`)
- Reference files over 100 lines lead with a table of contents
- No hard dependency on any single MCP server for delivery — providers are discovered at runtime and the skill falls back to paste/file/folder ingestion when none are available

If you edit this skill, re-run `evals/evals.json` end-to-end before reinstalling.
