---
name: voice-profile-generator
description: >
  Triggers on: "build my voice profile", "analyze my voice", "create a voice
  prompt from my transcripts", "make a voice skill from my writing", pasted
  Zoom/Meet/Granola transcripts, uploaded .txt/.md/.docx writing samples
  (blog posts, emails, LinkedIn posts, newsletters), or a folder path the user
  points at containing any combination of the above, submitted for voice
  analysis.
  Does NOT trigger for: generic writing help without voice profiling intent,
  editing a single piece in someone's voice when a profile already exists,
  transcribing audio, or TTS/voice cloning requests.
  Produces: a portable `[name]-voice-prompt.md` system prompt and a packaged
  `[name]-voice.skill` zip — consumed by the user in any LLM or installed as
  a native Claude skill.
---

# Voice Profile Generator

Analyzes voice transcripts and writing samples to produce a deployable voice profile — as a portable LLM system prompt and a native Claude skill file.

## Step 1 — Collect sources

Read [`references/source-ingestion.md`](references/source-ingestion.md) for file handling (pasted text, individual `.txt`/`.md`/`.docx` files, or a folder path the user points at), word-count thresholds, and the two confirmations to gather (name + content types) before analysis begins.

## Step 2 — Analyze voice

Read [`references/analysis-framework.md`](references/analysis-framework.md). Work through every one of the seven dimensions, pulling 2–4 verbatim examples from the source material for each. Flag any dimension where source material is insufficient.

## Step 3 — Generate outputs

Read [`references/output-templates.md`](references/output-templates.md). Produce both files, package the skill, and run the quality gate before delivering:

1. `[name]-voice-prompt.md` — portable system prompt, usable in any LLM
2. `[name]-voice.skill` — native Claude skill (zipped `[name]-voice/SKILL.md`)

## Step 4 — Deliver summary

After presenting files, briefly tell the user:
- 3–5 key voice characteristics identified
- Total word count and source types analyzed
- How to use each output file (paste the prompt, install the skill)
- How to improve fidelity over time (more material → re-run)

## Reference files

- [source-ingestion.md](references/source-ingestion.md) — Step 1
- [analysis-framework.md](references/analysis-framework.md) — Step 2
- [output-templates.md](references/output-templates.md) — Step 3

## Rules

- Never skip a dimension. If source material is thin, flag low confidence in that section instead of inventing traits.
- Every voice trait must trace to a verbatim quote from the source material.
- No template placeholders may remain in the final output files.
- Load one reference file per step, then proceed. Do not bulk-load all references at activation.
- Minimum ~2,000 words for a high-confidence profile. Proceed with less when asked, but flag low-confidence dimensions explicitly.
