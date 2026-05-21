---
name: rulebook-writing
description: >-
  This skill should be used when the user is writing, editing, or structuring a rulebook, player aid,
  quick-start guide, or back-of-box copy. Trigger on: "write the rulebook", "rules document", "teach
  order", "blind playtest", "player aid", "rules clarity", "component list", "setup diagram",
  "back of box copy", or any rules-writing and documentation question.
version: 0.1.0
---

# Rulebook Writing

Help a solo hobbyist designer turn a working game into a **rulebook** that strangers can read, understand, and play from — without the designer in the room.

This is the most underestimated skill in board game design. A great game with a bad rulebook will fail blind playtests, lose Kickstarter pledges, and accumulate "I returned it" reviews. A merely good game with an excellent rulebook will succeed.

## Operating mode: Socratic, but a craft

Rulebooks are a craft, not a frame. The coaching voice still applies — ask before prescribing — but rulebooks have *real conventions* that good designers follow. Don't reinvent the wheel.

When a user brings a draft, the first move is questions:

- Who's the audience? (Hobby gamers familiar with conventions vs. family/casual.)
- Has this been blind playtested? (Untested rules will be wrong; you can't write your way out of unclear design.)
- What's the comparable rulebook the user wants this to feel like? (Pull a real example.)
- What's currently failing — comprehension, teach time, look-up speed, or something else?

If the answer to "blind tested?" is no, name that the rulebook can't be finalized yet. Help them draft one to *use in* the next blind test.

## Rulebook structure (the canonical order)

There are stylistic choices, but the canonical structure for a hobby-game rulebook is:

1. **Cover and back-of-box copy** — title, evocative line, player count, age, time.
2. **Inside cover or page 1** — short intro: world flavor, the player's role, what they're trying to do. **Two paragraphs maximum.** Players are eager to start.
3. **Components list** — picture and count of every item in the box.
4. **Setup** — step-by-step, ideally with a diagram of the table state at end of setup.
5. **Game overview** — short. "On your turn, you do X. The game ends when Y. The winner is Z." This frames everything that follows.
6. **Turn structure / round structure** — the spine of the rules. Detail every phase a player goes through.
7. **Action types in detail** — each action gets its own subsection with rules, costs, examples.
8. **Specific rules** — combat, movement, scoring sub-systems, anything not covered in turn structure.
9. **End of game and scoring** — when does it end, how do you score, how to break ties.
10. **Reference sheets / appendix** — solo mode, advanced rules, FAQ, quick reference, designer notes (last).

Variations exist (campaign games front-load lore, party games drop straight into "how to play in 60 seconds"), but for most designs this order is what audiences expect. Deviating costs cognitive load.

## The two readers of a rulebook

Every rule has to work for two readers:

1. **The first-time reader**, learning the game alone.
2. **The mid-game looker-upper**, who needs to find a rule fast in turn 4.

Optimize for the first-time reader in the body. Optimize for the looker-upper with reference sheets, indices, and clear headings.

If a rule is hard to find for the looker-upper, players will skip it, get the rule wrong, and blame the game.

## Teach order vs. reference order

These are different. Teach order is what makes the game *learnable*. Reference order is what makes a rule *findable*.

A rulebook should be in **teach order** in its body, with **reference structures** layered in via headings, indices, page numbers, and player aids.

Common teach order:
1. The world / your role (motivation).
2. The goal (what you're trying to do).
3. The turn (what you do every round).
4. The actions (the verbs you can choose from).
5. The specifics (how each action resolves).
6. The end (when and how you win).

Setup goes near the front *because the box is open and players are eager*, but rules-wise it should ideally be read after the overview. Solve this with a "Read this first if you've never played" marker on the overview, and a "Now set up" marker on the setup section.

## Examples and diagrams: the highest-leverage pages

A rulebook with no examples is a math textbook. Examples and diagrams are where comprehension actually happens.

- **Worked turn example**. Show one full turn from start to finish, with text and diagram. This is the most-read page in any rulebook.
- **Diagrams for setup**. The end-state of setup, fully laid out, with arrows pointing to each item.
- **Diagrams for spatial mechanics**. Movement, range, line of sight, area of effect — anything spatial *needs* a diagram. Words alone fail.
- **Examples in action sub-sections**. Each action that has any nuance gets a 1-3 sentence example with a small visual cue.

For a worked rulebook template, see [rulebook-structure-template.md](../../references/rulebook-writing/rulebook-structure-template.md).

## Voice and writing style

For the rulebook proper:

- **Second person, active voice.** "On your turn, you take 2 actions." Not "the active player must take 2 actions."
- **Present tense.** "You draw 3 cards." Not "you will draw 3 cards."
- **Imperative for procedure.** "Draw a card. Reveal it. Place it in your row."
- **Short paragraphs.** 2-4 sentences. Lots of headings.
- **Bold or italicize key terms** the first time they appear, and use them consistently after.
- **Boxed callouts** for examples, exceptions, designer notes.
- **One rule per sentence** wherever possible.

Avoid:
- Passive voice.
- Sentences with embedded conditionals ("If a player has more than 3 cards, unless that player is the active player, in which case…" → split into two sentences and a header).
- Redundant phrasing ("In order to score points, the player must…" → "To score, …").
- "The player" / "a player" — use "you" for the reader.

For voice in the **introduction and flavor copy** (which is different from rules voice), see [voice-and-tone.md](../../references/rulebook-writing/voice-and-tone.md).

## Player aids and reference cards

Every game above the lightest weight needs **player aids** — small cards or sheets summarizing the turn structure and key actions.

Good player aid principles:

- **One card per player.** If they're sharing, no one looks at it.
- **Turn structure top, action menu middle, scoring bottom.** Standard pattern.
- **Iconography matches the rulebook and the cards.** Inconsistent icons are a real failure.
- **No new information.** If a player aid contradicts the rulebook, the rulebook wins, but ideally there's no contradiction.

A great player aid can carry a rulebook with a few rough edges. A missing or bad player aid puts all the load on the rulebook.

## FAQ and edge cases

If your blind playtests have surfaced consistent rules questions, those need to land in the rulebook *or* an FAQ section.

Rules of thumb:

- **Three or more testers asked the same question** → revise the main rules to prevent it.
- **One tester asked once** → consider an FAQ entry; don't pollute the main rules.
- **A weird interaction between two specific cards** → a card-text errata or a designer-notes appendix.

The FAQ is *not* a place to put rules you should have written better. Use it sparingly.

## Common rulebook failures

When the user's rulebook is failing blind playtests, run through these:

- **Setup is unclear.** Players assemble the wrong starting state. Almost always solvable with a setup diagram.
- **Turn structure is buried.** Should be one of the first three sections; should fit on a player aid.
- **Action effects are described separately from action costs.** Always pair them: "*Trade*: pay 2 wood, gain 3 coin."
- **Win condition is unclear or stated late.** Tell the player what they're trying to do *before* you tell them how to do it.
- **Iconography is introduced without legend.** All icons need a legend, ideally on the player aid.
- **Conditional rules buried in flavor text.** Anything mechanical must be in rules text, not flavor text.
- **Edge-case rules outweigh main rules.** If 30% of the rulebook is edge cases, either trim them or move them to an appendix.
- **Designer notes mixed with rules.** Move designer notes to the very end, separately marked.

For more, see [common-rulebook-failures.md](../../references/rulebook-writing/common-rulebook-failures.md).

## Editing pass: the one-hour rulebook revision

When the user has a draft and wants a tightening pass, walk them through this in order:

1. **Find every passive sentence**, rewrite active.
2. **Find every "the player" / "a player"**, change to "you" (with care for second-person/third-person consistency in the section).
3. **Find every embedded conditional** ("if X unless Y unless Z"), split into multiple sentences.
4. **Find every paragraph longer than 4 sentences**, look for split points.
5. **Find every rule without an example**, decide if it needs one.
6. **Find every term used in more than one way**, standardize to one term.
7. **Read every heading aloud**. Are they parallel? Is the document scannable from headings alone?
8. **Read the rulebook backward, section by section**, asking: "If I just landed here, would I know what's going on?"

This is mechanical work but it's the difference between a rulebook that works and one that frustrates.

## Other documents the rulebook ecosystem includes

- **Quick-start guide** — for complex games, a 1-2 page "first game" sheet that simplifies and points to the full rules later.
- **Reference card** — see player aids above.
- **Solo mode rules** — usually a separate booklet or appendix; never folded into main rules.
- **Campaign / scenario book** — separate from rulebook; sealed sections for legacy.
- **Back-of-box copy** — short, evocative, mentioning weight, time, count, age. Earns the buyer's interest.

For each of these, see [rulebook-structure-template.md](../../references/rulebook-writing/rulebook-structure-template.md).

## What to avoid

- **Don't write the final rulebook before blind playtesting the design.** Untested designs have wrong rules.
- **Don't rely on the rulebook to explain a confusing design.** If the rules need 50 pages, the design is too complex or the rules are poorly structured. Sometimes both.
- **Don't write designer voice into the rules body.** Save it for designer notes at the end.
- **Don't underweight the components list and setup.** The first impression is "open the box, look at the parts." Get those right.
- **Don't ship without a player aid.** Especially for any game above the lightest weight.

## Handing off

- The rulebook reveals a design problem (a rule that can't be written cleanly because the rule itself is broken) → back to [mechanics-design](../mechanics-design/mechanics-design.md).
- The user wants the rulebook to feel more in-world → [narrative-worldbuilding](../narrative-worldbuilding/narrative-worldbuilding.md) for voice and intro flavor.
- The user wants iconography, layout, and visual design → [art-direction](../art-direction/art-direction.md).

Name the handoff explicitly.
