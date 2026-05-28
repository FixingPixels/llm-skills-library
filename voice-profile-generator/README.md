# Voice Profile Generator

A Claude Agent Skill that analyzes someone's voice transcripts and writing samples and produces a deployable voice profile in two formats:

1. **`[name]-voice-prompt.md`** — a portable system prompt you can paste into any LLM (ChatGPT, Claude, Gemini, etc.) and immediately get output that sounds like you.
2. **`[name]-voice.skill`** — a packaged Claude Agent Skill (a zipped `[name]-voice/SKILL.md`) that triggers natively in Claude when you ask it to write in your voice.

This repo is the authoring source. The runtime install lives at `~/.claude/skills/voice-profile-generator/`.

## What it does

Given enough source material, the skill works through a seven-dimension voice analysis (signature, sentence architecture, lexical fingerprint, structural patterns, rhetorical moves, what-this-voice-is-NOT, and signature examples) and produces evidence-backed output files. Every trait it asserts is traceable to a verbatim quote from the source material.

## Triggers

Any of these will activate the skill:

- "build my voice profile", "analyze my voice"
- "create a voice prompt from my transcripts"
- "make a voice skill from my writing"
- Pasted Zoom / Meet / Granola transcripts
- Uploaded `.txt` / `.md` / `.docx` writing samples (blog posts, emails, LinkedIn posts, newsletters)

It does **not** trigger for generic writing help, single-piece edits when a profile already exists, transcription, or TTS / voice cloning requests.

## How to use it

### Install

```bash
# From this repo
mkdir -p ~/.claude/skills/voice-profile-generator
rsync -a --delete SKILL.md references evals learnings.md \
  ~/.claude/skills/voice-profile-generator/
```

### Run

In any Claude session with skills enabled, give it your source material in any of these forms:

- Paste transcripts or writing directly into the chat.
- Attach individual `.txt`, `.md`, or `.docx` files.
- **Point at a folder** — e.g. "use the files in `~/voice-samples/`". The skill will recursively enumerate supported files, read each one, and report a per-file inventory (with anything unsupported listed as skipped so you can convert and re-run).

Then say:

> "Build my voice profile."

The skill will:

1. Tally your sources and tell you the total word count, including a per-file breakdown when you point at a folder.
2. Classify each source as transcript or written sample (using folder name, filename, and content-shape signals) and ask you to confirm any ambiguous ones.
3. Ask for the name to use in filenames and which content types you'll be writing (LinkedIn, newsletter, blog, etc.).
4. Run the seven-dimension analysis, pulling 2–4 verbatim examples per dimension.
5. Generate both output files and run a quality gate before delivery.
6. Summarize the 3–5 most distinctive voice characteristics identified.

#### Folder layout that classifies cleanly

If you organize your folder like this, classification is automatic:

```
~/voice-samples/
├── transcripts/
│   ├── 2025-09-podcast-episode.txt
│   └── granola-team-meeting.md
└── writing/
    ├── blog/
    │   └── post-about-pricing.md
    └── newsletter/
        └── issue-12.md
```

A flat folder also works — the skill will use filename keywords and content shape (speaker labels, timestamps, filler words) to classify each file.

### Recommended source volume

| Source words | Confidence |
|--------------|------------|
| ~2,000+ | High — all dimensions usable |
| 1,000–2,000 | Medium — structural dimensions may be flagged |
| Under 1,000 | Low — skill will proceed if asked, but will flag low-confidence dimensions explicitly |

Mix transcripts and written samples when possible. Transcripts capture authentic rhythm and unedited idea structure; written samples capture intentional craft choices like openings and closings.

## Repository layout

```
voice-profile-generator/
├── SKILL.md                          # Tier-2 routing document
├── README.md                         # This file
├── references/
│   ├── source-ingestion.md           # Step 1 — file handling, word counts, confirmations
│   ├── analysis-framework.md         # Step 2 — seven-dimension framework
│   └── output-templates.md           # Step 3 — output templates, packaging, quality gate
├── evals/
│   └── evals.json                    # Three realistic test prompts
└── learnings.md                      # Self-improvement notes (pruned weekly)
```

The skill follows the progressive disclosure architecture from Anthropic's [skill authoring best practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices):

- **Tier 1** — YAML frontmatter in `SKILL.md` is always loaded into context (~150 tokens).
- **Tier 2** — `SKILL.md` body is loaded when the skill activates (~56 lines).
- **Tier 3** — Reference files load one at a time, only at the step that needs them.

## Output files

### `[name]-voice-prompt.md`

A self-contained system prompt (minimum 800 words) covering voice signature, sentence structure, vocabulary (reach-for and avoid lists), opening patterns, argument architecture, closings, rhetorical moves, what the voice is NOT, signature examples, and writing instructions with a self-review checklist.

Paste it into any LLM as a system prompt and you should immediately get recognizable output.

### `[name]-voice.skill`

A zipped Claude skill containing `[name]-voice/SKILL.md`. The embedded SKILL.md includes the full voice profile inline (not by reference) plus optional Content Type Notes for each format you said you'd be writing.

To install:

```bash
unzip [name]-voice.skill -d ~/.claude/skills/
```

After that, just say "draft a LinkedIn post about X" or "write this email in my voice" and the skill triggers automatically.

## Improving fidelity over time

Add more source material and re-run. Each run is a fresh analysis — there's no incremental update mode. The new profile replaces the old one. As you collect more transcripts and writing, low-confidence dimensions (especially structural ones, when only transcripts are available) firm up.

## Tests

Three realistic test prompts live in [`evals/evals.json`](evals/evals.json):

1. ~1,500 words of transcripts only — should flag low-confidence structural dimensions.
2. Multiple `.md` blog posts with declared content types — should produce a skill with Content Type Notes.
3. 400 words of source material — should proceed if asked but flag every low-confidence dimension and recommend adding more material.

Run them as a regression check after editing the framework or templates.

## Authoring conventions

This skill is built per the [skill-architect](file:///Users/ccollett/.claude/skills/skill-architect/) golden rules:

- `SKILL.md` body under 200 lines (currently 56)
- YAML description has Triggers / Does NOT trigger / Produces parts
- All references linked one level deep with explicit `references/...` paths
- Each reference has its own frontmatter (`title`, `load_at`, `summary`)
- Reference files over 100 lines lead with a table of contents
- No hard dependency on any single MCP server for delivery

If you edit this skill, run the validation checklist in the plan before reinstalling.
