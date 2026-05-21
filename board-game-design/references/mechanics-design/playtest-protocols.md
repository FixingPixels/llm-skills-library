# Playtest Protocols

Most solo hobbyists know they need to playtest. They don't know what *kind* of test to run or what to look for. This is a structured guide.

## The five test types

Each tests a different thing. Don't blend them — you'll get muddy data.

### 1. Solo test (designer alone)

You play multiple sides yourself.

- **Good for**: Catching broken rules, math errors, scoring loops, missed edge cases. The fastest, cheapest test.
- **Bad for**: Anything social — interaction, fun, table feel, downtime.
- **Run it**: Before any group test. After every rule change. Multiple times.
- **Watch for**: Rules you can't remember, situations you didn't plan for, math that doesn't add up.

### 2. Hot-seat test (designer + close collaborator)

Two people, designer present, the rules are explained mid-play if needed.

- **Good for**: Iterating quickly. The designer can tweak rules in real time and re-run a turn.
- **Bad for**: Pacing data, accessibility, "would I buy this" judgment.
- **Run it**: After solo testing surfaces no obvious breakage. As often as possible.
- **Watch for**: Decisions that feel hard, decisions that feel obvious, the moment your collaborator's energy shifts.

### 3. Group playtest (designer present, group of 3-5)

Real game. Designer can teach but otherwise sits back.

- **Good for**: Pacing, social dynamics, AP, kingmaker, runaway leaders, fun-as-experienced.
- **Bad for**: Catching rules ambiguity (designer is present to clarify).
- **Run it**: Every 2-3 weeks during active development.
- **Watch for**: Where attention drifts. Who seems checked out. Where the table goes quiet (boredom or AP) vs. loud (engagement). The score curve over rounds. The moment in the middle where energy dips.

### 4. Blind playtest (designer absent or silent, group teaches itself)

Group is given the rulebook (or video) and plays without designer help.

- **Good for**: Rulebook clarity, real out-of-box experience, judging whether the game stands alone.
- **Bad for**: Iterating mid-test (the whole point is to *not* intervene).
- **Run it**: Once the design feels stable enough to ship. Multiple groups, ideally strangers.
- **Watch for**: Rules they got wrong, rules they couldn't find, questions they had to invent answers to. Their post-game verdict.

### 5. Stress test

Targeted test of one specific scenario — extreme player counts, edge-case combos, rules-lawyer scenarios.

- **Good for**: Closing known holes before publishing.
- **Bad for**: General balance signal.
- **Run it**: Late, when polishing.
- **Watch for**: Whether the edge case breaks the game, slows it, or just feels weird.

## Playtest hypothesis template

Every playtest should have a written hypothesis before play begins. Example:

> **Hypothesis**: The trade action is too strong; players will take it on >60% of available turns and trading-focused players will outscore others by 15+ points.
>
> **What I'll measure**: Action selection per turn (tally sheet); final scores; player feedback on which actions felt strongest.
>
> **Decision rule**: If the hypothesis confirms, reduce trade reward from 3 to 2 OR increase trade cost. If it's close (50% utilization), leave alone, retest with different group.

## What to record

In real time, during play:

- **Game length** (start, end, time per round if possible).
- **Action selection** — quick tally of which actions each player took.
- **Score by round** if there's a public score track.
- **Specific moments** — note time + what happened ("Round 4: Alice complains about waiting, scores tied at 12-11-9").

After play, in the debrief:

- **Verdict question** — "Want to play again?" Be specific: today, this week, ever. The answer matters.
- **Best/worst moment** — "What was the moment you most enjoyed? What was the moment you most disliked?"
- **What was confusing** — "When did you have to ask a rules question?"
- **What felt strong/weak** — "Which action would you take more / less of?"
- **What was missing** — "What did you wish you could do that the game wouldn't let you?"

## What *not* to do during playtest

- **Don't apologize.** "I know this part is rough" trains players to be polite.
- **Don't explain why a rule is wrong.** Watch them break it and learn from that.
- **Don't tell them about future versions.** Test the game in front of them.
- **Don't sell them the experience.** Let them have it or not.
- **Don't ask leading questions.** "Was the trade action too strong?" → "Which actions felt strongest? Which felt weakest?"
- **Don't change rules mid-game** in group tests. (Hot-seat is different.) You'll lose the data.

## After the test

Wait 24 hours before redesigning. Hot reactions are often wrong. Sleep on what you saw, then change *one* thing.

If multiple testers reported the same problem, that's a signal. If one tester reported a problem and others didn't, that's noise — note it and watch for it next test.

## Solo design without group access

Hobbyists without playtest groups can use:

- **Tabletop Simulator / Tabletopia** — for remote tests with online groups.
- **Print-and-play forums** — BGG print-and-play forum, r/tabletopgamedesign, designer Discords.
- **Local game stores** — many host designer playtest nights.
- **Game design conventions** — Protospiel, Unpub, etc. exist specifically for this.
- **Asynchronous solo "AI" play** — for pure mechanical balance, you can model the game and run it mentally or in a spreadsheet, but this never substitutes for human play.
