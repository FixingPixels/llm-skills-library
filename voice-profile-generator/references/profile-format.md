---
title: Profile Format
load_at: mode-a-step-3
summary: Structure of the living references/voice-profile.md (metadata header, profile body, changelog), merge rules for incremental updates, and the single-file quality gate
---

# Profile Format

Defines the structure of the one canonical file this skill produces and maintains:

```
references/voice-profile.md
```

There is no portable prompt file, no zipped `.skill`, no second artifact. This document is the format spec for that one file, plus the rules for merging new evidence into it on every update.

## Contents

1. [File location and resolution](#1-file-location-and-resolution)
2. [Template for first build](#2-template-for-first-build)
3. [Merge rules for updates](#3-merge-rules-for-updates)
4. [Changelog conventions](#4-changelog-conventions)
5. [Quality gate](#5-quality-gate)

---

## 1. File location and resolution

The profile lives inside this skill at `references/voice-profile.md`. When the skill is installed, that resolves to:

```
~/.claude/skills/voice-profile-generator/references/voice-profile.md
```

If the skill is being used from the authoring repo directly, it resolves to:

```
<repo-root>/references/voice-profile.md
```

Always resolve the path relative to the SKILL.md being executed, so the same logic works in both locations.

If the file does not exist, treat the current run as a first build (Mode A from scratch) — create it from the template in [§2](#2-template-for-first-build).

---

## 2. Template for first build

On a first build, write `references/voice-profile.md` using this template. Fill every section with specific, evidence-backed content from the analysis. No placeholders — if a dimension is uncertain, say so explicitly inside that section.

Minimum body length: **800 words** (excluding the metadata header and changelog).

```markdown
---
profile_version: 2
name: [Full Name]
display_name: [First Name]
content_types: [comma-separated list, e.g. "LinkedIn posts, newsletter, blog"]  # optional, omit if not supplied
last_synced:
  # One entry per provider the profile has ever pulled from. Add a new entry
  # the first time a provider yields material. Update only the entries for
  # providers that successfully ran in the current update. Omit this map
  # entirely on a fresh fallback-only build.
  granola: [ISO 8601 datetime or null]
  fireflies: [ISO 8601 datetime or null]
  # ...and so on for any other provider used
cumulative_word_count: [integer total across all sources ever analyzed]
sources:
  - id: [provider id, file path, or "pasted-2026-05-30"]
    type: [transcript | written]
    origin: [provider | file | pasted | url]
    provider: [granola | fireflies | otter | fathom | read.ai | tldv | grain | zoom | meet | teams]  # required when origin = provider; omit otherwise
    title: [meeting title, filename, or short label]
    date: [ISO 8601 date]
    words: [approximate word count]
confidence:
  voice_signature: [high | medium | low]
  sentence_architecture: [high | medium | low]
  lexical_fingerprint: [high | medium | low]
  structural_patterns: [high | medium | low]
  rhetorical_moves: [high | medium | low]
  voice_is_not: [high | medium | low]
  signature_examples: [high | medium | low]
---

# Voice Profile: [Full Name]

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

[Prose or tight list. Off-register tones, never-used constructions, structural taboos, and specific AI patterns absent from this person's writing. Make it actionable — a writer should be able to use this as a checklist of things to avoid.]

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
3. [Continue — aim for 6–8 specific instructions drawn from the analysis]

**Self-review checklist before submitting any draft:**
- [ ] Does the opening feel like one of [First Name]'s openings?
- [ ] Is the sentence rhythm right — varied, not uniform?
- [ ] Does the vocabulary feel native, not AI-flavored?
- [ ] Any phrases from the "Avoid" list?
- [ ] Does the closing land the way [First Name] closes things?
- [ ] Is the energy level correct?

---

## Content Type Notes
<!-- Omit this section entirely if no content types were supplied. -->

### [Content Type 1, e.g. LinkedIn Posts]
[Format, typical length, hook pattern, whether [First Name] uses CTAs, etc.]

### [Content Type 2, e.g. Newsletter]
[Structure, storytelling ratio, depth, etc.]

---

## Profile Update Log

<!-- Newest entry first. One block per update. See profile-format.md §4 for conventions. -->

### [ISO 8601 datetime] — Initial build
- Sources: [N items, X words] from [list of providers and/or files/pasted]
- Confidence baseline established for all 7 dimensions.
- [Any low-confidence dimensions and why.]
```

---

## 3. Merge rules for updates

On every update (Mode A on an existing profile, or an in-session "update my profile with that" from Mode B):

1. **Re-read the existing profile first.** Treat it as the prior state. Do not regenerate from scratch.
2. **Touch only what the new material justifies.** If a dimension is unchanged by the new material, leave it alone.
3. **Refine and add evidence; do not wipe.** New verbatim examples can join existing ones. Existing findings stay unless the new material directly contradicts them — in which case explain the contradiction in the changelog and update the section.
4. **Raise confidence as evidence accumulates.** When new material pushes a low-confidence dimension over the line (more written samples lifting structural patterns, more transcripts firming up pacing, etc.), update the `confidence` field in the metadata header.
5. **Update metadata.** For each provider that successfully ran in this update, bump `last_synced[provider]` to that provider's newest source date for this run. Do not touch entries for providers that were unavailable this run. Append new source entries to `sources` (each with the correct `origin` and, when applicable, `provider` field). Recompute `cumulative_word_count`.
6. **Preserve `name`, `display_name`, and `content_types`.** Only change them when the user explicitly asks.
7. **Append a changelog entry.** Always. See [§4](#4-changelog-conventions).
8. **No portable prompt, no zip.** This file is the artifact. Do not regenerate a second file.

---

## 4. Changelog conventions

Append to the **top** of the `Profile Update Log` section (newest first). One block per update.

Use one of these update kinds:

- **Provider sync** — incremental pull from one or more transcript providers (Granola, Fireflies, Zoom, etc.). Name the providers involved in this update.
- **Manual sources** — paste/file/folder ingestion (no provider, or a folder of provider-agnostic files).
- **In-session update** — voice signals captured during a Mode B writing session.

Block shape:

```markdown
### [ISO 8601 datetime] — [Update kind]: [providers or short label]
- Sources added: [N items, X words; break down by provider when multiple, e.g. "3 Granola + 2 Fireflies + 1 Zoom"]
- Dimensions touched: [list, e.g. "Lexical Fingerprint, Closings"]
- Notable changes:
  - [One bullet per substantive change. Cite the new verbatim evidence where relevant.]
- Confidence changes: [e.g. "Structural Patterns: low -> medium"] or "None."
- last_synced updated: [list of providers whose watermark moved, e.g. "granola, fireflies"; "None" for manual / in-session]
```

The changelog is what lets the user (and future runs) audit how the profile evolved. Never collapse or rewrite past entries.

---

## 5. Quality gate

Before declaring an update done (first build or incremental), verify all of:

- [ ] `references/voice-profile.md` exists at the correct path and parses as Markdown with a valid YAML frontmatter header.
- [ ] Every section in the body is filled — no template placeholders, no `[bracketed instructions]` remain.
- [ ] Every voice trait is traceable to a verbatim quote from the source material (Granola, file, pasted, or captured in-session correction).
- [ ] "What This Voice Is NOT" names specific AI patterns absent from the source.
- [ ] Body length is at least 800 words (excluding frontmatter and changelog).
- [ ] Low-confidence dimensions are flagged in-section AND reflected in the `confidence` metadata.
- [ ] Metadata header is internally consistent: for every `last_synced[provider]`, the value equals the newest `sources[*].date` where `provider == provider` (or is `null` if that provider has no sources yet); `cumulative_word_count` matches the sum of `sources[*].words`; every `sources[].origin = provider` entry has a `provider` field, and entries with other origins do not.
- [ ] A changelog entry has been appended at the top of the Profile Update Log.
