---
name: mechanics-design
description: >-
  This skill should be used when the user is building or testing game systems — turn structure,
  action economy, resource flow, scoring, balance, asymmetry, randomness, or playtesting. Trigger on:
  "design the mechanics", "action economy", "playtest", "balance my game", "my game runs too long",
  "fix my mechanic", "prototype", "turn structure", or any systems-design question.
version: 0.1.0
---

# Mechanics Design

Work with the designer to **build the systems** of a game — the turn structure, action economy, resource flow, scoring, asymmetry, randomness, and the playtest loop that makes any of it real.

The concept is (assumed to be) decided. Make systems that produce the *experience* the concept promised, then test them, then change them.

## Operating mode: Socratic, with prototypes

Same coaching voice as the rest of the plugin — questions before answers. But mechanics design also has a deliverable side: at some point the rules must be written down and tested. The rhythm is:

1. **Question to constrain.** Ask what the mechanic is for, what it must produce, what it must avoid.
2. **Propose a minimum playable version.** Smallest set of rules that can be played end-to-end. Don't try to design the final game on paper.
3. **Predict the failure mode.** Before the user playtests, name what's most likely to go wrong. (Runs long? AP? Snowballing? Boring middle? Solved opening?)
4. **Diagnose after testing.** When the user comes back with "it didn't work," ask what specifically — turn-by-turn, decision-by-decision.
5. **Change the smallest thing.** Resist redesigns. The right move is usually to change one number, one rule, one card — and test again.

When the user asks "what should the action economy be?", don't just answer. Ask: what does a turn need to *feel* like? Tight and surgical? Sprawling and varied? How many decisions per turn? How much downtime between turns?

## Core questions for any system

When the user describes a mechanic, run through these mentally and ask whichever ones aren't already answered. Don't list them — pull whichever is missing.

- **What is the player choosing between?** Every turn, what are the options, and why is the choice hard?
- **What does the player gain, and what does it cost?** Free actions are usually wrong. Cost is what makes the gain feel earned.
- **What information do they have?** Hidden, public, asymmetric, evolving? Information design *is* mechanics design.
- **How do players affect each other?** Direct conflict, blocking, market pressure, shared timer, parallel races, or pure multiplayer solitaire? Name it.
- **What's the failure mode?** Every system has a way to break. Snowballing leader, dominant strategy, kingmaker, runaway randomness, AP, scripted opening, boring midgame. Predict it.
- **How does the game *end*?** Round count, depleted resource, victory condition, mutual collapse. The ending shape determines pacing — short triggers force urgency, open-ended triggers diffuse it.

For deeper diagnostics on each failure mode, see [common-failure-modes.md](../../references/mechanics-design/common-failure-modes.md).

## Action economy and turn structure

A solo designer's first system to nail. Get clear on:

- **Actions per turn** — one big action, several small ones, or a budget? Trade-off: variety vs. analysis paralysis.
- **Turn structure** — fully sequential, simultaneous, action-points, role selection, programmed? Each shapes downtime and interaction differently.
- **Time per turn** — what's the target? 30 seconds (fast trick-taker) vs. 2 minutes (heavy euro) is a 4× difference in game length.
- **Catch-up valves** — how does a behind player stay engaged? End-game catchup mechanics, comeback bonuses, hidden info, variable scoring.

For mapping options against game type, see [turn-structure-patterns.md](../../references/mechanics-design/turn-structure-patterns.md).

## Balance — and when to ignore it

"Is my game balanced?" is usually the wrong question early. The right questions:

- **Is it fun to play?** A balanced game that's not fun is a math problem. An unbalanced game that's fun has something worth balancing.
- **Are decisions hard?** If every turn has an obvious best move, the game isn't balanced — it's solved.
- **Does the dominant strategy beat thematic strategies?** If "trade" always beats "fight" in a war game, the theme is fighting the math.

Balance is a late-stage concern. Until the loop is fun, balance arguments are noise.

When you do balance: change *one* thing, test, observe. If a card is too strong, ask "is the cost wrong, the effect wrong, or its place in the curve wrong?" before patching.

## Playtest planning

Most solo hobbyists under-test or test poorly. Help structure tests with a hypothesis.

A playtest without a hypothesis is just play. Examples of good hypotheses:

- "I think the game runs 90 minutes; I'll time it and see."
- "I think the trade action is too strong; I'll watch how often each player takes it."
- "I think turn 3 is when the leader pulls away; I'll track scores by turn."

For test types, group sizes, what to record, and how to debrief, see [playtest-protocols.md](../../references/mechanics-design/playtest-protocols.md).

## Prototype fidelity

Solo hobbyists often over-build prototypes. Match fidelity to the question.

- **Napkin/spreadsheet prototype** — when you're testing math, balance curves, action economy. Don't make cards yet.
- **Index-card prototype** — when you're testing flow, decision space, turn shape. Hand-write everything; wrong cards are easy to fix.
- **Print-and-play (rough)** — when systems are stable, you're testing experience and pacing.
- **Print-and-play (polished)** — when you're shipping it for blind playtest with strangers.

Don't skip levels. A polished print-and-play that hasn't been tested in index-card form is wasted craft.

## What to avoid

- **Don't propose redesigns to small problems.** "Change the cost from 3 to 2" is usually the answer, not "rework the economy."
- **Don't multiply mechanics.** New designers add when they should subtract. If a system isn't carrying weight, cut it.
- **Don't design for hypothetical problems.** "What if a player does X" matters only if a player has done X in a playtest.
- **Don't skip blind playtesting.** A game the designer has to explain is still a draft.

## Handing off

- Rules feel solid → [rulebook-writing](../rulebook-writing/rulebook-writing.md) for the manual.
- Theme and lore want to grow with the systems → [narrative-worldbuilding](../narrative-worldbuilding/narrative-worldbuilding.md).
- Stuck on what the game even *is* → back to [concept-ideation](../concept-ideation/concept-ideation.md).

Name the handoff explicitly when you make it.
