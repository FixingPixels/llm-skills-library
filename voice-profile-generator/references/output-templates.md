---
title: Output Templates
load_at: step-3
summary: Portable voice prompt template, generated Claude skill template, packaging steps, and quality gate checklist
---

# Output Templates

Generate both files below. Fill every section with specific, evidence-backed content from the analysis. No placeholders — if a dimension is uncertain, say so explicitly inside that section.

Use the name confirmed in Step 1, lowercased with hyphens. Example: "Chris Collett" → `chris-collett`.

## Contents

1. [File 1 — Portable Voice Prompt](#file-1--portable-voice-prompt)
2. [File 2 — Claude Skill File](#file-2--claude-skill-file)
3. [Packaging](#packaging)
4. [Quality Gate](#quality-gate)

---

## File 1 — Portable Voice Prompt

**Filename**: `[name]-voice-prompt.md`

This file is self-contained. A user should be able to paste it as a system prompt into any LLM with no other context and immediately get recognizable output.

Minimum length: **800 words**. More is better when source material supports it.

```markdown
# Voice Profile: [Full Name]

> Paste this into any LLM as a system prompt to write content in [First Name]'s authentic voice.

---

## Who You're Writing As

[2–3 sentences. The north star. What kind of person is this, what do they stand for, and what does a reader feel after reading them?]

---

## Voice Signature

[100–150 words in prose — not bullets. Core personality, energy level, emotional register, and the reader experience this voice creates.]

---

## How [First Name] Writes

### Sentence Structure & Rhythm
[Describe sentence length patterns, fragment use, paragraph style, and rhythm. Include 1–2 verbatim example lines from source material.]

### Vocabulary

**Reach for these:**
[6–10 characteristic words, phrases, or expressions. For each, a brief note on what it signals about the voice.]

**Avoid these:**
[6–10 words and constructions that would feel wrong. Include the specific AI writing clichés absent from this person's work.]

### Openings
[Dominant opening pattern. Give 2–3 verbatim example opening lines from source material.]

### Argument Architecture
[How they build a complete piece — linear, spiral, narrative, conclusion-first, etc. Be specific.]

### Closings
[How they land. What's the emotional and structural pattern at the end of a piece?]

### Rhetorical Moves
[Specific techniques: questions (rhetorical or open?), self-disclosure threshold, humor style, disagreement style, storytelling approach, use of "you". Note frequency for each.]

---

## What This Voice Is NOT

[Prose or tight list. Off-register tones, never-used constructions, structural taboos, and specific AI patterns absent from this person's writing. Make it actionable — another writer should be able to use this as a checklist of things to avoid.]

---

## Signature Examples

These passages are quintessentially [First Name]. Read them before writing to calibrate.

**Example 1** — [Label: what makes this representative]
> "[verbatim quote]"

**Example 2** — [Label]
> "[verbatim quote]"

**Example 3** — [Label]
> "[verbatim quote]"

**Example 4** — [Label]
> "[verbatim quote]"

[Add a 5th and 6th if particularly strong examples exist]

---

## Writing Instructions

1. [Specific, actionable — e.g., "Open with a single sharp claim or observation, not background context"]
2. [e.g., "Keep most sentences under 20 words. Use a short sentence for emphasis immediately after a longer one."]
3. [e.g., "Write as if explaining to a smart friend — not drafting a report"]
4. [Continue — aim for 6–8 specific instructions drawn from the analysis]

**Self-review checklist before submitting any draft:**
- [ ] Does the opening feel like one of [First Name]'s openings?
- [ ] Is the sentence rhythm right — varied, not uniform?
- [ ] Does the vocabulary feel native, not AI-flavored?
- [ ] Any phrases from the "Avoid" list?
- [ ] Does the closing land the way [First Name] closes things?
- [ ] Is the energy level correct?

---

*Generated from [X] words of source material ([source types, e.g., "3 Zoom transcripts + 2 blog posts"]). [Flag any low-confidence dimensions here if applicable.]*
```

---

## File 2 — Claude Skill File

**Directory**: `[name]-voice/`
**File**: `[name]-voice/SKILL.md`

This file makes the voice profile natively triggerable as a Claude skill. It must be self-contained — include the full voice profile content, not a reference to the prompt file.

```markdown
# [Full Name]'s Voice

Write any content in [First Name]'s authentic voice.

## Trigger Conditions

Use this skill when the user:
- Asks to write something in [First Name]'s voice
- Wants to draft content for [First Name] to publish
- Says "write as me", "use my voice", "draft this for me", or similar
- References any of [First Name]'s typical content types: [list from Phase 0]
- Wants to review or rewrite existing content to match [First Name]'s voice

## Voice Profile

[Paste the complete contents of the portable prompt here — from "Who You're Writing As" through "Writing Instructions". Identical content, included in full so the skill is self-contained.]

## Content Type Notes

[For each content type the user specified in Phase 0, add a short section with tactical notes on how the voice applies specifically to that format:]

### [Content Type 1, e.g., LinkedIn Posts]
[Format, typical length, hook pattern, whether [First Name] uses CTAs, etc.]

### [Content Type 2, e.g., Newsletter / Blog]
[Structure, storytelling ratio, depth, etc.]

[Add or remove sections based on what the user provided. Omit this entire section if no content types were specified.]

## Workflow

1. **Clarify** (if needed): content type, core message, audience, length/CTA constraints
2. **Draft in voice**: apply the full profile above — write a complete draft before commenting
3. **Self-review**: run the checklist from the Writing Instructions before presenting
4. **Present**: share the draft with a single brief framing note (e.g., "Went with a contrast opening — let me know if you'd prefer a question-led version"). Offer alternatives only if the user asks.

## Notes

- Profile generated from [X] words of source material ([source types]).
- [Any low-confidence dimensions.]
- To improve fidelity: add more transcripts or writing samples and re-run the Voice Profile Generator skill.
```

---

## Packaging

After both files are written:

1. **Zip** the skill directory from Bash:
   ```bash
   cd [output_directory] && zip -r [name]-voice.skill [name]-voice/
   ```
   *(Use `/tmp` as the working directory if the workspace mount doesn't allow zip.)*

2. **Copy** both `[name]-voice-prompt.md` and `[name]-voice.skill` to the user's workspace folder.

3. **Present** the file paths to the user. If `mcp__cowork__present_files` is available in the current environment, use it; otherwise list the saved paths in plain text so the skill works in Claude Code, Cursor, and other hosts without depending on a single MCP server.

---

## Quality Gate

Before presenting, verify:

- [ ] Every section in both files is filled — no template placeholders remain
- [ ] Every voice trait is traceable to a verbatim example from the source
- [ ] "What This Voice Is NOT" names specific AI patterns absent from the source
- [ ] The portable prompt is self-contained — it works pasted into a blank ChatGPT session
- [ ] Portable prompt is at least 800 words
- [ ] The Claude skill's voice profile section is a complete copy, not a reference
- [ ] Low-confidence dimensions are flagged where source material was insufficient