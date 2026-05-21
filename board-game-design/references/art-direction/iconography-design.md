# Iconography Design

Iconography is the most-used visual asset in any game above the lightest weight. Done well, it's invisible. Done badly, it's the single most common reason for "this game is hard to play."

## Inventory first

Before designing icons, list every concept that needs one:

- **Resources** — wood, stone, grain, gold, etc.
- **Actions** — move, build, trade, attack, etc.
- **Effects** — gain X, lose X, swap, draw, discard.
- **Conditions** — if/when triggers, exhausted, hidden.
- **Score categories** — VP, end-game bonus, special trophies.
- **Player elements** — first-player marker, player color slot, asymmetric power glyph.
- **Phase / time markers** — round counter, era indicator, end-trigger.
- **Modifiers** — +1, ×2, half, max, min.
- **Locations / zones** — hand, deck, discard, market.

A thorough inventory often reveals 40-80 icons in a moderately complex game. That's a substantial design problem.

## The four properties of a working icon

Every icon should have:

1. **Meaning** — what concept does this represent?
2. **Silhouette** — what shape is it, and how distinct is that shape from every other icon's shape?
3. **Color** — primary, secondary; does the color reinforce the meaning?
4. **Scale tolerance** — does it still read at the smallest size it'll appear?

Test all four for every icon. The third and fourth fail most often.

## Silhouette test

Pull every icon to a single color (black silhouette on white). If you can't tell them apart in silhouette, the icons aren't visually distinct.

Most amateur iconography fails this test — the icons look great in color but mush together in silhouette. Players, especially in a busy game state, are often distinguishing icons by silhouette before color.

## Color test

Pull every icon to grayscale. Can color-blind players distinguish them? 8% of men have some form of color blindness; deuteranopia (red-green) is the most common. Designs that rely on red vs. green discrimination fail for this audience.

Add color-blind-safe contrast: shapes, patterns, or letters/numbers as backup distinctions.

## Scale test

Print or render the icon at the actual size it'll appear on the smallest component (often the back of a card, or in a column on a player aid). If it doesn't read at print size, it doesn't work.

A common failure: icons designed at 200px on screen that need to render at 12px on a card. The detail evaporates.

## Iconographic grammar

Beyond individual icons, you need a grammar — rules for how icons combine.

Common grammars:

- **Modifier-resource**: `+1` next to a wood icon means "gain 1 wood." `−2` next to a stone icon means "lose 2 stone."
- **Conditional triggers**: a rounded rectangle around an icon means "when this happens, …"
- **Time / sequencing**: a small clock or arrow indicates ordering.
- **Choice operators**: `OR` between two icons (or a slash, or a stylized fork) for "pick one."
- **Cost-effect arrows**: `[cost]` → `[effect]` shown in a horizontal flow.

Pick a grammar and apply it consistently across cards, board, rulebook, and player aids. Inconsistent grammar (a `+` here, the word "gain" there) is a classic amateur mistake.

## Common iconography mistakes

- **Too many icons.** Some games would be cleaner with text on key cards. Iconography is great for repeated concepts; not great for one-off effects.
- **Icons trying to convey complex effects.** "If a player has more than 3 gold and is adjacent to a forest, they may discard 2 cards to gain a worker" — that's text, not icon.
- **Inconsistent style.** Some icons are flat, some illustrated, some traced from photography. Pick one approach.
- **Color-collision.** Two icons that read the same in color (e.g., orange wheat and orange wood). Differentiate.
- **Cute-but-confusing.** A cute illustrated icon that takes a moment to identify is worse than a clean abstract icon. Cuteness is not the goal.
- **Borrowed iconography.** Using icons that have established meanings in the hobby (e.g., the universally-recognized "VP star") and then meaning something else with them.

## When to use text instead

Icons are great for: frequently repeated concepts, multiplied effects, language-independence.

Text is better for: one-off rules, complex conditional effects, anything that requires precision.

Don't iconify everything. A card that says "Gain 2 wood, then if you have at least 5 stone, draw a card" is clearer in text than in five stacked icons. Use icons where they pay rent.

## Iconography across surfaces

Icons must look identical across:

- Cards
- Board
- Player aids
- Rulebook
- Box-back
- Reference cards
- Score sheet

A small variation in iconography between surfaces is a real failure. Build a master vector source for every icon and pull it into all surfaces from there.

## Quick test: the cold reader

Take your iconography sheet to a non-player. Show them five icons in isolation. Ask:

- "What do you think this means?"
- "Which of these would you guess is more powerful?"
- "Which two of these go together?"

If they don't get it within a few seconds for the most-used icons (resources, gain/lose, primary actions), redesign. Players in real games have less attention than a cold reader, not more.

## Design tools and resources

- **Vector source mandatory.** SVG, AI, PDF — anything scalable. Raster icons can't be re-used at multiple sizes.
- **Icon libraries as starting points.** game-icons.net is a CC-licensed source of public-domain game icons. Often used as a base for custom work.
- **Test in the actual game.** A test print of the player aid and a single card of each type reveals 90% of iconography problems.
