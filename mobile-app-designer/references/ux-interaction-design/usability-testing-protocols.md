# Usability Testing Protocols

Most solo builders know they should test with users. They don't know what *kind* of test to run or what to look for. This is a structured guide.

## The five test types

Each tests a different thing. Don't blend them — you'll get muddy signal.

### 1. Self-test (builder alone)

You use your own app as a new user — ideally on a fresh install, fresh account, or a device you haven't tested on before.

- **Good for**: Catching broken flows, copy errors, loading states you forgot to design, empty states that don't make sense. Fast and free.
- **Bad for**: Finding the things you're blind to from familiarity. You know too much; you'll skip steps unconsciously and not notice.
- **Run it**: Before any external test. After every significant change. On a physical device, not just the simulator.
- **Watch for**: Any moment where you have to think for half a second about what to do. Any screen that looks different on a real device than it did in Figma. Any flow that requires you to remember something from a previous step.

### 2. Hallway test (unscripted, 5–15 minutes)

Hand your phone to someone nearby — a friend, a family member, a colleague who hasn't seen the app. Give them a task. Watch silently.

- **Good for**: Fast signal on obvious problems. Anything that confuses a smart person who knows nothing about your app is a real problem. Cheap to run, no setup required.
- **Bad for**: Nuanced signal about whether the app delivers sustained value. This audience will be polite and quick.
- **Run it**: As often as possible during active design. Every time you think "this is obviously clear," run a hallway test to check.
- **Watch for**: Where they hesitate. What they tap that you didn't expect. What they say out loud unprompted. Whether they find the feature you just built without being told it's there.

### 3. Moderated usability test (3–5 participants, you observe)

A structured session: give the participant a task, watch them work through it, ask follow-up questions after. You're present but not helping.

- **Good for**: Deep signal on a specific flow. Understanding *why* users behave the way they do, not just that they do. Finding the precise point in a flow where comprehension breaks.
- **Bad for**: Quick iteration — takes time to recruit and schedule. Not suitable for early-stage flows that will change significantly before anyone else sees them.
- **Run it**: When a flow feels stable enough to test properly. Three to five participants will surface 80% of the major usability problems.
- **Watch for**: The exact moment hesitation occurs — which element, which word. Tasks they abandon. Strategies they invent because the designed path wasn't clear. Their vocabulary for describing what they expected.

**What not to do during a moderated test**:
- Don't explain why something works the way it does.
- Don't ask leading questions: "Did you find the filter button helpful?" → "What did you do when you wanted to narrow the results?"
- Don't rescue them when they're stuck — watch and note exactly where they got stuck.
- Don't defend design decisions in the session. Save reactions for after.

### 4. Unmoderated remote test (builder absent, recorded)

Participants complete tasks without you present, using tools like Maze, Lyssna, UserTesting, or TestFlight with screen recording. You review recordings and metrics after.

- **Good for**: Testing the real out-of-box experience. Removing your presence bias (users behave differently when watched). Reaching people who match your actual target user profile.
- **Bad for**: Understanding *why* something happened — you can see what users did but you can't ask follow-up questions in real time.
- **Run it**: When a flow feels stable enough to be close to the real product. Use regularly to catch regressions after significant updates.
- **Watch for**: Task completion rates, time on task, drop-off points. Replay recordings looking for hesitation, backtracking, and unexpected paths. Compare what users did to what you expected.

### 5. Edge-case / regression test

Targeted test of specific conditions: empty states, offline behaviour, slow network, old device, first-time vs. returning user, extreme content lengths.

- **Good for**: Closing known holes before a release. Catching regressions introduced by new builds.
- **Bad for**: General signal — this is about closing specific risks, not finding new ones.
- **Run it**: Before every significant release. Maintain a list of edge cases found in previous tests.
- **Watch for**: Empty states that show incorrect or missing UI. Actions that work on fast networks but spin or fail on slow ones. Text that breaks layout when it's longer than your test data. Anything that behaves differently on an iPhone SE (small screen) vs. a Pro Max.

---

## Test hypothesis template

Every test should have a written hypothesis before you start. Example:

> **Hypothesis**: Users won't understand that the filter icon in the top-right corner opens category filters — they'll either ignore it or not find it when asked to filter by category.
>
> **What I'll observe**: Where users look first when asked to filter. Whether they find the icon or try another path. How long it takes.
>
> **Decision rule**: If two or more of five participants don't find the filter or express confusion, redesign the affordance — either move it, add a label, or add an empty-state hint.

Writing the hypothesis makes you more honest about what you learn. It's easy to rationalise ambiguous observations in favour of the design you built. The hypothesis gives you a decision rule before your judgement is clouded.

---

## What to record

During the test:

- **The task** (exact wording given to the participant).
- **Time to complete** (or time before abandonment).
- **The path taken** — note every tap in sequence if you can.
- **Specific moments** — note the exact screen and action where anything interesting happened ("tried to tap the label instead of the button", "asked 'is this the right place?'").
- **Exact words** — what they said unprompted is gold. Write it down verbatim.

After the test, before looking at notes:

- **Your overall impression**: Did they get it? Where was the hardest moment?
- **The single most surprising thing** you observed.

Then review notes systematically.

---

## After the test

Wait before redesigning. Immediate reactions after a difficult test session are often wrong — you'll be tempted to rebuild everything when you need to change one thing.

If multiple participants struggled with the same thing, that's a signal. If one participant struggled and others didn't, that's noise — note it and watch for it in the next round.

Change the smallest thing that addresses the signal, then test again. A complete redesign between every test session means you're never actually learning from data — you're just iterating on instinct with extra steps.

---

## Testing without access to users

Solo builders without easy access to test participants can use:

- **Maze / Lyssna** — recruit panels for unmoderated remote tests; small per-response cost.
- **TestFlight / Play Store internal testing** — distribute to anyone with the link; ask for feedback on a specific flow.
- **Reddit / Discord communities** — niche communities related to your app's problem space are often willing to give quick feedback if asked honestly.
- **X / Twitter** — brief demo + specific question ("I'm testing this flow — does this button label make sense?") can get fast responses.
- **Fake door test** — add a button or feature entry point before building the feature; measure tap rate to validate interest before investing.
