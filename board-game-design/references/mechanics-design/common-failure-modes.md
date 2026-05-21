# Common Failure Modes

Diagnostic guide for the most frequent ways board game systems break. When a designer reports something feels off, walk through these and find the match.

## Runaway leader / snowballing

**Symptom**: Whoever pulls ahead in turn 2-3 wins. Other players know it and disengage.

**Diagnoses**:
- Resources convert into more resources with no plateau (positive feedback with no negative).
- Scoring rewards what you already have (vs. what you newly do).
- No mechanism for trailing players to disrupt the leader.

**Fixes to try**:
- Diminishing returns on the dominant resource conversion.
- End-game scoring categories that reward variety, not concentration.
- Targeted disruption (steal, block, attack) available cheaply enough that trailing players can use it.
- Catch-up bonuses (last-place player draws extra, gets first action, etc.) — careful, can feel patronizing.

## Kingmaker

**Symptom**: A player who can't win decides who does. Often emerges in the last turn or two.

**Diagnoses**:
- Direct attack actions with no opportunity cost.
- Endgame visibility too high (everyone can see who's leading and pile on).
- Scoring thresholds where one cube swings the win.

**Fixes to try**:
- Hide endgame scoring (hidden objectives, end-game bonuses revealed late).
- Make attacks costly enough that a losing player benefits from *not* attacking arbitrarily.
- Multiple paths to win so a single attack doesn't decide it.

## Analysis paralysis (AP)

**Symptom**: Turns drag. Some players stare at the board for minutes.

**Diagnoses**:
- Too many options at once (combinatorial explosion).
- Decisions are too consequential (one wrong move feels like losing).
- Information is too perfect (player can compute optimum if they try hard enough).

**Fixes to try**:
- Cap action choices per turn (you may take 2 of these 5 actions, not all of them).
- Force timing (sand timer, simultaneous action, drafting).
- Add hidden info so optimal computation is impossible — players have to act on instinct.
- Reduce decision weight by making turns more frequent and smaller.

## Multiplayer solitaire

**Symptom**: Players don't watch each other. Turns are fast but uninteresting.

**Diagnoses**:
- No shared resources, market, or board.
- No public information that affects others' choices.
- Scoring is purely individual with no comparison.

**Fixes to try**:
- Shared draw pool, shared market, or shared limited supply.
- Public actions that broadcast intent.
- Bidding, drafting, or auction layer over independent engines.
- End-game scoring categories where players compete (most of X scores 5, second-most scores 3).

## Boring middle

**Symptom**: Opening is interesting, end is exciting, middle is players grinding.

**Diagnoses**:
- Engine is built and the game becomes execution.
- No new information enters mid-game (all cards seen, all routes known).
- Pacing has no second-act event.

**Fixes to try**:
- Phase changes (era 2 unlocks new actions, new cards enter mid-game).
- Mid-game scoring events (round 3 of 6 has a scoring round, forcing positioning).
- Random or triggered events that change the optimal play mid-game.
- Tighter game length — sometimes the middle is "boring" because the game is too long.

## Solved opening

**Symptom**: Experienced players make the same first three moves every time.

**Diagnoses**:
- One opening is genuinely best by the math.
- Setup is identical each game — no variability forces fresh thinking.

**Fixes to try**:
- Variable setup (different starting resources, different objective cards, modular board).
- Hand of cards drawn at start that varies what's optimal.
- Asymmetric player powers that punish a one-size opening.

## Dominant strategy

**Symptom**: One path always wins. "Always rush the spice trade" or similar.

**Diagnoses**:
- The path's reward is too high or its cost too low.
- Other paths have higher variance with no upside to compensate.
- The path scales — early advantage compounds.

**Fixes to try**:
- Increase the cost of the dominant action (resource cost, opportunity cost).
- Add a counter — players can punish concentration on this path.
- Cap how often the action can be taken per round.
- Test whether the alternate paths are actually balanced *with each other*, even if all are weaker than the dominant one — sometimes you need to nerf the dominant *and* boost two weak paths.

## Runaway randomness

**Symptom**: Game outcomes feel arbitrary. Players say "the dice decided."

**Diagnoses**:
- High-variance events with no mitigation.
- Critical decisions hinge on a single roll.
- No way to spend resources to influence outcomes.

**Fixes to try**:
- Reroll mechanics (spend a token to reroll, take 2 of 3 dice).
- Probability mitigation (fewer big rolls, more small ones; bell curves over flat distributions).
- Player input *after* randomness (draw 3 cards then choose, not flip 1 card and react).
- Convert pure randomness into *managed* randomness — same uncertainty, more agency.

## The game is too long

**Symptom**: Sessions end with people checking phones; everyone leaves saying "good game" but no one wants to play again.

**Diagnoses**:
- Round count too high.
- Each turn takes longer than designed.
- End-game trigger is too distant.
- Scoring is too elaborate (tallying takes 10 minutes).

**Fixes to try**:
- Cut a round. Then test. Then cut another. Most prototypes are 30% too long.
- Tighten turn structure (fewer choices per turn, faster decisions).
- Move the end-game trigger closer.
- Simplify scoring — public running totals beat end-game tally.

## Diagnostic prompts to ask the designer

When they report a problem, before you propose a fix:

- "At what turn did it go wrong?"
- "What were players doing in the broken phase — staring, executing, fighting?"
- "Did one player win by a lot, by a little, or did everyone feel close?"
- "What did people say after the game ended?"
- "If you played again tomorrow, would they want to?"
