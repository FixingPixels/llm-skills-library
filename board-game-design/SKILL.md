---
name: board-game-design
description: >-
  This skill should be used when the user is designing, iterating, or shipping a tabletop board game
  as a solo hobbyist. Trigger on: "I'm making a board game", "help me design a game", "review my rules",
  game concept pitches, hook development, theme and mechanic fit, turn structure, action economy,
  playtesting and balance, worldbuilding, factions, flavor text, saturation and comparables,
  BGG/Kickstarter positioning, rules writing, blind playtest failures, art briefs, iconography, and
  box cover design. Framework-light and Socratic. Uses training knowledge unless the user explicitly
  asks for live market or web research.
version: 0.1.0
---

# Board Game Design

Use this skill when the user is **designing, iterating, or shipping a tabletop game** — especially as a **solo hobbyist** — from raw idea through prototype, narrative, market fit, rulebook, and visual identity.

## Voice

Coach **Socratically**: ask before answering, push for specificity, cite **concrete games and working designers** rather than abstract frameworks. Prefer “what does this designer do here” over MDA-style diagrams unless the user asks for theory.

## Workflow

1. **Infer the lens** from what the user is doing (router below).
2. **Open the matching skill** and follow its mode, avoids, and handoffs.
3. **Open reference files** only when the skill points to them — `references/<skill-name>/...`.

Name handoffs explicitly (e.g. “Applying [mechanics-design](skills/mechanics-design/mechanics-design.md) for…”).

## Skill router

| User intent | Skill |
|-------------|-------|
| Idea, hook, core fantasy, theme/mechanic pairing, elevator pitch | [concept-ideation](skills/concept-ideation/concept-ideation.md) |
| Systems, turns, economy, balance, playtests, failure modes | [mechanics-design](skills/mechanics-design/mechanics-design.md) |
| Lore, factions, flavor, theme at the table, campaigns | [narrative-worldbuilding](skills/narrative-worldbuilding/narrative-worldbuilding.md) |
| Genre, audience, comparables, saturation, positioning | [trends-analysis](skills/trends-analysis/trends-analysis.md) |
| Rulebook structure, teach order, examples, player aids, BOB copy | [rulebook-writing](skills/rulebook-writing/rulebook-writing.md) |
| Art briefs, style, icons, layout, components, covers | [art-direction](skills/art-direction/art-direction.md) |

## Web research

Default: **no live web lookup** — use training knowledge and user files. For **current** BGG/Kickstarter/releases or fresh competitor lists, wait until the user explicitly asks, then search or fetch as available.

## Limitations

Does not replace **playing games in the target space**, **blind playtests**, **professional artists**, or **business/legal publishing decisions**.

## Source of truth

Each skill lives in `skills/<name>/<name>.md`. Reference material lives in `references/<name>/`.
