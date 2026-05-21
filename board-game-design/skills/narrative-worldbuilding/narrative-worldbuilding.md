---
name: narrative-worldbuilding
description: >-
  This skill should be used when the user is developing world lore, factions, flavor text, campaign
  narrative, or theme integration for their game. Trigger on: "worldbuilding", "lore", "factions",
  "flavor text", "card names", "campaign narrative", "theme integration", "asymmetric powers",
  "story arc", or any question where theme, fiction, or narrative is the focus.
version: 0.1.0
---

# Narrative & Worldbuilding

Help a solo hobbyist designer make the **fiction** of their game work — world, lore, characters, factions, story arc, flavor text, asymmetric powers — so the theme is *experienced*, not decorated.

Most board game theme is wallpaper. Push the designer toward narrative that the mechanics *make happen* and that gives players reasons to remember the game.

## Operating mode: Socratic, theme-as-design

Same coaching voice. But narrative work has its own trap: designers either treat theme as decoration (paint it on at the end) or treat it as a novel (write 50 pages of lore that never appears at the table).

Neither is right. Theme is design. Every faction, every card name, every illustration, every rule should tell the same story. Keep asking: **does this show up at the table?**

When the user says "I want a faction of moss-druids," ask:
- What does playing a moss-druid *feel* different from? What can they do that no one else can, and what *can't* they do?
- What does a moss-druid player tell their friend they did? "I built engines" is decoration. "I was the moss-druid, so when I sat too long, the forest grew over my opponents' supply lines" is design.

## What narrative actually has to do at the table

Three jobs, ranked:

1. **Make decisions feel meaningful.** The player isn't moving cubes; they're making a *choice* the world cares about. Theme makes the cubes mean something.
2. **Generate memorable moments.** When the box closes, what does the player retell? Theme is the engine of that retelling.
3. **Do *not* contradict the mechanics.** When a designer says "diplomacy" and the mechanic is "trade cubes," theme and design are at war. Players notice.

If a piece of narrative doesn't do one of those three jobs, it's wallpaper. Ask: where does this show up at the table? If the answer is "the rulebook intro," cut or relocate it.

## Core questions for any narrative work

When the user asks for help on theme/lore/world, work these in:

- **What's the player's role?** Not just "leader of a faction" — what *kind* of person, with what desires and what limits?
- **What's the world's central tension?** A world without conflict has no game. Where does the world hurt? What's broken? Who's losing?
- **What's the time horizon?** A single battle, a generation, an era? Time horizon dictates pacing of the narrative arcs.
- **What does the player *not* control?** The world is made by what the player can't change — the weather, the law, the gods, the economy.
- **What changes over the game?** A static world is a board. A dynamic world is a story. What is *different* in turn 10 vs. turn 1?

## Theme integration tools

The plugin's bias is **framework-light**. Don't pull MDA. Talk like a designer.

For a working set of integration prompts and examples, see [theme-as-design.md](../../references/narrative-worldbuilding/theme-as-design.md).

## Asymmetric factions and characters

If the game has asymmetry (different powers, different starting conditions), each faction should answer:

- **Why does this faction exist in this world?** Not their power — their *role in the fiction*.
- **What do they want that other factions don't?** Different goals, not just different paths to the same goal.
- **What can they do that no one else can?** Mechanical asymmetry that *means* something thematically.
- **What can't they do?** The constraint is as identity-defining as the power.
- **What do they sound like?** Voice, naming conventions, visual signature — even one or two clues is enough.

Push back on factions that are "the fast one, the strong one, the smart one." That's mechanical asymmetry pretending to be narrative. Ask: who *are* they? See [faction-design-prompts.md](../../references/narrative-worldbuilding/faction-design-prompts.md).

## Flavor text and card names

These are the highest-leverage narrative surfaces in most games — players read them every turn. Most flavor text is wasted: ornamental, generic, or contradicting the card effect.

Good flavor text:
- **Earns its space.** If it doesn't add to the player's understanding of the world or the moment, cut it.
- **Speaks in the world's voice**, not the designer's. Prefer in-world quotes, in-world fragments, in-world details.
- **Explains the mechanic implicitly** when possible. A card called "Famine Year" with effect "all players lose 2 grain" needs no flavor — the name *is* the flavor *is* the mechanic.

Card names matter more than flavor text. A great card name does the work of a paragraph. Push the user to find the noun that *is* the card. "Defensive Wall (+2 defense)" is weak. "Last Stand" is sharper.

## Campaign and legacy structure

If the game has a campaign or legacy structure, narrative carries 80% of the weight. Players will forgive uneven mechanics in a campaign if the story pulls them forward; they will not forgive uneven story.

Key questions for campaign design:

- **What's the through-line?** One sentence describing the arc from session 1 to session N.
- **What changes session-to-session?** Both mechanically and narratively. If sessions feel the same, the campaign is a long game in disguise.
- **What's reversible vs. permanent?** Permanent change (Legacy-style) creates investment. Reversible change (modular campaigns) creates replayability. Pick.
- **How do you handle losing players?** Branching, catchup, narrative explanations. Don't punish failure with content lockouts — players will retire the game.
- **What's the ending?** Open-ended campaigns die. Plan the last session first.

## What to avoid

- **Don't write lore that won't appear at the table.** A 10-page world bible is a designer's pleasure, not a player's experience.
- **Don't reskin tropes without earning them.** "Like Lord of the Rings but with cyberpunk elves" is a pitch, not a world. Push for what's specific to *this* game.
- **Don't let theme contradict mechanics.** If a "stealth" mechanic is just "fewer defense dice," call it out — the fiction is fighting the math.
- **Don't pile on factions.** Six factions, each different, is rarely better than three factions, each fully realized.
- **Don't design heavy lore alone.** Theme that lands is theme that survived someone else asking "what does that mean?" Test it.

## Handing off

- Theme is locked, mechanics need to absorb it → [mechanics-design](../mechanics-design/mechanics-design.md).
- World is rich enough, time to write the manual → [rulebook-writing](../rulebook-writing/rulebook-writing.md) (especially the rulebook intro and reference sheets).
- Theme needs a visual identity → [art-direction](../art-direction/art-direction.md).

Name the handoff explicitly.
