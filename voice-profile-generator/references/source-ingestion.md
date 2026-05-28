---
title: Source Ingestion
load_at: step-1
summary: Collect transcripts and writing samples; handle .txt/.md/.docx; confirm name and content types before analysis
---

# Source Ingestion

Handle Step 1 of the voice profile workflow: gather all source material, compute the inventory, and confirm two facts with the user before moving to analysis.

## 1. Accept any of the following sources

| Source type | How to ingest |
|-------------|---------------|
| Pasted text in chat | Use directly — no tool call needed |
| `.txt` or `.md` files | Read tool |
| `.docx` files | Bash + `python-docx` (`python -c "from docx import Document; print('\n'.join(p.text for p in Document('file.docx').paragraphs))"`) |
| A folder path the user points at | See "Folder ingestion" below |
| Pasted URLs to public posts | WebFetch when the host allows it; otherwise ask the user to paste the text |

### Folder ingestion

When the user gives a folder path (e.g. "use the files in `~/voice-samples/`"):

1. Use Glob to enumerate supported files recursively: `**/*.{txt,md,docx}` under the given path.
2. Read each match using the per-extension method above.
3. List any unsupported files (`.pdf`, `.rtf`, `.html`, audio, video, etc.) in the inventory report under a "Skipped" line so the user can convert and re-run if needed. Do not silently drop them.
4. Sort surviving sources deterministically (alphabetical by relative path) before analysis so re-runs are reproducible.

### Classifying each source

Treat each item as one of two categories:

- **Transcripts** — Zoom, Google Meet, Granola, or any recording platform. Reveal authentic rhythm, vocabulary under pressure, and unedited idea structure.
- **Written samples** — blog posts, emails, LinkedIn posts, newsletters, any intentional prose. Reveal craft choices: openings, closings, edited vocabulary.

When ingesting from a folder, classify each file using these signals (in order):

1. **Folder name**: a parent directory matching `transcripts?`, `calls?`, `meetings?`, `zoom`, `meet`, `granola`, `interviews?` (case-insensitive) → transcript. A parent matching `posts?`, `blog`, `newsletter`, `emails?`, `writing`, `drafts?` → written sample.
2. **Filename**: same keyword patterns applied to the filename itself.
3. **Content shape**: speaker labels (`Chris:`, `[Speaker 1]`, `00:14:32`), filler words ("um", "uh"), and lack of paragraph structure → transcript. Headings, intentional paragraph breaks, polished sentences → written sample.

If classification is ambiguous for any file, list those files explicitly in the inventory report and ask the user to confirm before running the analysis. Do not guess silently.

## 2. Compute and report the inventory

For each source, note its type and approximate word count. Tell the user the total before continuing.

- **High confidence threshold**: ~2,000 words across all sources.
- Below threshold: proceed if asked, but flag in advance which dimensions will be low-confidence (typically Dimensions 4 and the closing-style portion of 7 when only transcripts are available).

## 3. Confirm two facts before Phase 1

Do not start analysis until both are answered:

1. **Name** — how should it appear in output files? (first name, full name, or handle). This becomes the lowercased-with-hyphens filename prefix (e.g., "Chris Collett" → `chris-collett`).
2. **Content types** — what will this profile be used to write? Examples: LinkedIn posts, blog articles, email newsletters, X threads, sales emails. The list drives the optional Content Type Notes section in the generated skill.

If the user does not specify content types, omit that section in Step 3 rather than inventing one.
