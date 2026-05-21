# Common Rulebook Failures

Diagnostic guide for rulebooks that aren't working. Match the symptom to the failure mode and propose targeted fixes.

## Failure: Players set up wrong

**Symptom**: Blind testers consistently begin the game with the wrong starting state.

**Root causes**:
- Setup is described in prose, not numbered steps.
- No diagram of the end-state of setup.
- Setup steps are out of order (you can't do step 4 until step 6).
- Setup is mixed with rules (players can't tell what they're doing yet vs. what they'll do later).

**Fixes**:
- Use a numbered list. One action per step.
- Add a labeled diagram of the table at end of setup.
- Re-read the steps cold and execute them with components on a table — find the order error.
- Move all rules out of the setup section.

## Failure: Players don't know the goal

**Symptom**: Three rounds in, a tester asks "wait, how do I win?"

**Root causes**:
- Game overview is missing or buried.
- Win condition is in the last section instead of stated up front.
- The overview is about the world, not the goal.

**Fixes**:
- Add a Game Overview page near the front. State the win condition in two sentences.
- Repeat the win condition at the end of the rulebook in the End of Game section.
- Make sure the player aid mentions the win condition.

## Failure: Players forget rules mid-game

**Symptom**: Mid-game, players ask rules questions that were answered on page 7.

**Root causes**:
- Rules are scattered across the rulebook.
- No player aid, or the player aid is incomplete.
- Iconography isn't doing the work — text-only rules don't hold in memory.

**Fixes**:
- Make a player aid that summarizes turn structure, actions, and scoring.
- Use icons consistently across cards, board, and rulebook.
- Add a one-page reference at the back of the rulebook.

## Failure: Rules contradict each other

**Symptom**: Players find two rules that say different things; they don't know which to follow.

**Root causes**:
- A general rule and a specific rule are both stated without a precedence rule.
- Card text says one thing, rulebook says another.
- An old rule from a previous draft wasn't deleted.

**Fixes**:
- State a precedence rule in the rulebook ("Card text overrides rulebook text" is standard).
- Search the rulebook for every variation of a key term and reconcile.
- Add a "Common Questions" or FAQ to address the conflict if it can't be resolved cleanly in the body.

## Failure: Comprehension drops in mid-rulebook

**Symptom**: Testers do fine for the first five pages, then start getting lost.

**Root causes**:
- The rulebook front-loads simple things and back-loads complex things, but doesn't bridge.
- New terms are introduced without definition.
- Page layout becomes denser as the rulebook progresses.

**Fixes**:
- Define every new term the first time it appears, in bold or italic.
- Maintain consistent layout density throughout — don't compress the back.
- If a section is genuinely complex, break it into smaller subsections with examples between.

## Failure: Players disengage during long teaches

**Symptom**: When the designer teaches the game, players check phones during the explanation.

**Root causes**:
- The teach is going through the rulebook in order, which isn't optimal for verbal teaching.
- Too much mechanical detail before the players know what they're doing.
- No table-based examples during the teach.

**Fixes**:
- Provide a "How to Teach" guide as a sidebar or appendix. The teach order is *not* the read order.
- Common teach order: world (1 sentence) → goal (1 sentence) → turn (1 sentence) → action types (1 sentence each) → "any questions, then we'll start" → rules-as-needed during play.
- Write a teach script the designer can use verbally.

## Failure: Edge cases dominate the rulebook

**Symptom**: 30%+ of the rulebook is "but if X, then Y" rules. Tests get bogged down.

**Root causes**:
- The design itself has too many edge cases (the rulebook is reflecting a design problem).
- Edge cases are interleaved with main rules instead of separated.
- The designer fears any unclear case and writes rules for things that haven't happened.

**Fixes**:
- Move all edge cases to an appendix or FAQ at the back.
- Look at the design — can edge cases be collapsed into general rules?
- Cut edge cases that haven't actually come up in playtests.

## Failure: New players freeze on first turn

**Symptom**: After the teach, players sit and stare. No one wants to take the first action.

**Root causes**:
- Too many actions available with no guidance.
- The opening is genuinely solved or seems-solved, and players are afraid to be wrong.
- The rulebook didn't suggest opening moves or strategies.

**Fixes**:
- Add a "Your First Game" section with suggested opening moves.
- Add a gentle "tip" boxed callout: "On your first few turns, focus on [generic strategy]."
- For complex games, provide a quick-start variant for the first game.

## Failure: Players dispute scoring

**Symptom**: At the end of the game, players argue about how to score, miscount, or arrive at different totals.

**Root causes**:
- Scoring is in prose instead of a list.
- Iconography is inconsistent (a card icon doesn't match the scoring sheet).
- Bonuses are scattered through different sections.

**Fixes**:
- One scoring section, all bonuses listed, all in the same icon vocabulary.
- A scoring example with diagrams.
- A scoring sheet as a tear-off or print-and-play companion.

## Failure: Veteran players "house-rule" the game

**Symptom**: After a few plays, groups change rules to fix what they perceive as broken.

**Root causes**:
- The design has a real problem the rulebook can't paper over.
- The rulebook described the rule unclearly and the group is "playing the wrong rule."
- A common edge case isn't addressed and groups invent a fix.

**Fixes**:
- If the rule is right but unclear: rewrite for clarity.
- If the rule is wrong: this is a mechanics-design problem, not a rulebook problem.
- Address the edge case explicitly if it comes up consistently.

## Failure: Online reviews complain about the rulebook specifically

**Symptom**: Reviews mention "the rulebook is bad" without specifying.

**Root causes**:
- Usually one of the failures above, multiplied.
- Often: missing player aid, missing diagrams, no end-of-setup picture.

**Fixes**:
- Read your top-3 reference rulebooks (games you admire) and note what they do that yours doesn't.
- Get fresh blind playtesters and watch them read.
- Consider a v2 with the changes — many publishers issue rulebook updates after release.
