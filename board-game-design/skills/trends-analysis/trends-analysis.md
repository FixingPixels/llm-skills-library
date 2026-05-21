---
name: trends-analysis
description: >-
  This skill should be used when the user wants to understand the board game market, audience fit,
  genre saturation, comparable games, or positioning for a publisher or crowdfunding pitch. Trigger on:
  "market research", "comparable games", "is this genre saturated", "BGG trends", "Kickstarter positioning",
  "genre conventions", "audience", "has this been done before", or any competitive landscape question.
version: 0.1.0
---

# Trends Analysis

Help a solo hobbyist designer understand the **board game market and audience** — what's been done, what's selling, what's saturated, what's underserved, and where their game lives in the landscape.

**Important constraint**: This skill defaults to working from training knowledge and any files the user provides (BGG exports, sales reports, competitor rulebooks). It does **not** automatically perform web research. If the user wants live data — current BGG hotness, recent Kickstarter campaigns, this month's releases — they must explicitly ask. Then use web search or fetch tools available in the environment.

## Operating mode: Socratic, with concrete games

The coaching voice is Socratic. For trends work, that means: don't just list "10 hot 2025 trends." Ask what the user is *actually* trying to learn — usually one of:

1. **"Has someone already made this?"** (Originality check.)
2. **"Will anyone want this?"** (Audience check.)
3. **"How do I describe this to a publisher / a Kickstarter audience?"** (Positioning.)
4. **"What does the genre expect?"** (Convention check.)
5. **"Where's the gap I could ship into?"** (Opportunity.)

Different questions, different answers. Identify which one before analyzing.

## The first move: name the comparison set

When a user asks about trends or market fit, the first move is usually: *what existing games are the closest comparisons?* Without comparisons, trends analysis is hand-waving.

If the user knows: ask them to name 3-5 closest cousins.
If the user doesn't know: that's a problem. They're designing in the dark. Help them list adjacent games, and gently flag that they should be playing more games in their target space.

The comparison set unlocks every other analysis.

## What "trends" actually means

Trends in tabletop are slow. The hobby moves in years, not weeks. Real trends to know about (as of training knowledge):

- **Cozy games** — *Wingspan*, *Cascadia*, *Dorfromantik*, *Verdant*. Soft, beautiful, low-conflict, satisfying engines.
- **Solo modes as standard** — most mid-weight new releases ship with solo modes. Audiences expect it.
- **Legacy and campaign games** — *Pandemic Legacy*, *Gloomhaven*, *Oath*, *Sleeping Gods*. Long-form play, evolving state.
- **Roll-and-write / flip-and-write** — light footprint, fast play, often abstract.
- **Word games revival** — *Decrypto*, *Just One*, party-adjacent designs.
- **Heavier-than-Pandemic co-ops** — *Spirit Island*, *Aeon's End*, *The Crew*. Co-ops that aren't "newbie" games.
- **18xx and economic resurgence** — long but devoted audience.
- **Dexterity games** — *Flick 'em Up*, *Catacombs*, *Junk Art*. Not big but not dead.
- **Crowdfunding maturation** — Kickstarter is no longer the easy money it was 2014–2018; Gamefound, BackerKit, and direct-to-retail compete; deluxification ("ALL THE MINIS") is fatiguing some backers.
- **AI and digital-companion concerns** — designers and audiences increasingly suspicious of AI art on Kickstarter; theme matters.

For more granular genre-by-genre observations, see [genre-conventions.md](../../references/trends-analysis/genre-conventions.md).

## Saturation analysis

When the user asks "is this genre saturated?", reframe. Saturation isn't binary. The question is:

1. **Is there demand?** Active players, online communities, recent successful releases.
2. **Is there shelf space?** Specifically — does the audience need *another* one, or is the niche full?
3. **What's the threshold to break through?** What does a new entrant have to do better than the existing leaders?

Examples:

- "Cozy nature euros" — high demand, somewhat saturated. New entrants need to do something the existing leaders don't (different scale, different theme angle, different mechanics).
- "Trick-taking with twists" — moderately demanded, surprisingly under-served at the high end. *The Crew* showed there's appetite. New entrants have room.
- "Zombie survival" — very saturated. Demand has cooled. New entrants need a strong hook to overcome audience fatigue.
- "Dexterity games" — undersaturated. Small demand, small shelf space, but the gap is real if your game is good.

For a structured scan, see [market-fit-checklist.md](../../references/trends-analysis/market-fit-checklist.md).

## Audience identification

A common solo hobbyist mistake: designing for "everyone." Push for specificity.

Useful audience axes:

- **Weight** — light family (Catan-or-lighter), midweight gateway (Wingspan, Splendor), heavy (Brass, Spirit Island).
- **Length tolerance** — under 30 min, 30–60, 60–90, 90+, evening-long.
- **Player count sweet spot** — 1, 2, 3-4, 5-6, party (7+).
- **Conflict tolerance** — low (cozy/cooperative), medium (indirect competition), high (direct attack, take-that, war).
- **Strategic depth** — casual (light decisions), strategic (hard decisions matter), simulationist (the world model is part of the appeal).
- **Theme preference** — fantasy, sci-fi, historical, abstract, real-world contemporary, cozy/nature.
- **Aesthetic preference** — cute/cartoon, painterly/illustration, photorealistic, abstract/graphic, retro.

A tight audience profile is two or three axes locked. "Midweight, 60-min, 1-3 player, cozy nature theme" is specific enough to position. "A strategy game for everyone" is not.

## Positioning

If the user is working on a pitch — to a publisher, to backers, to a playtest community — push for these:

- **The one-sentence pitch.** "It's a [weight] [genre] for [player count] where you [verb] in order to [goal]." Short.
- **The two-comparable pitch.** "If you like *[X]* and *[Y]*, you'll like this because [the new thing]." Use real games.
- **The differentiator.** What does this do that nothing else does? One thing, named precisely.
- **The audience.** Who's buying? "Cozy euro fans who want a 2-player option." Specific.

Don't let the user position vaguely. "It's like *Wingspan* but better" is not a position. "It's *Wingspan* for two players, in 30 minutes, with a campaign arc" is.

## When to refer the user to live research

Trigger live web research (with explicit user consent) when:

- The question depends on **current** state ("what's hot on BGG this month," "did anything ship in this niche this year," "what's funding on Kickstarter right now").
- The question is about **specific recent games** the user names that postdate training.
- The user wants competitive landscape for a publisher pitch and freshness matters.

Otherwise, training knowledge plus the user's own experience is the right grounding. Be honest about what you don't know — "I know the hobby through [training cutoff]; for what's released since, we'd need to look it up."

## What to avoid

- **Don't fabricate sales numbers, BGG ratings, or Kickstarter results.** If you don't know, say so. The user's design will be based on this — wrong data is harmful.
- **Don't claim a niche is "untapped" without evidence.** Most "no one has made this!" claims are wrong. Push the user to look harder.
- **Don't over-trust BGG hotness.** It reflects the BGG audience (heavier, more hardcore than the broader market). Mass-market games often underrepresented.
- **Don't moralize about the market.** Deluxification, Kickstarter fatigue, AI art concerns are real, but the user can have their own view. Inform, don't preach.
- **Don't replace playing games.** Trends analysis is no substitute for the user actually playing 50+ games in their target space.

## Handing off

- The user is questioning whether the concept is original → back to [concept-ideation](../concept-ideation/concept-ideation.md).
- The user wants to write a pitch document or campaign page → that's [rulebook-writing](../rulebook-writing/rulebook-writing.md) (it covers pitch and back-of-box copy too).
- The user wants visual positioning vs. competitors → [art-direction](../art-direction/art-direction.md).

Name the handoff explicitly.
