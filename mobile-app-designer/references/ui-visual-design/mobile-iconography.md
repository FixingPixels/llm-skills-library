# Mobile Iconography

Iconography is the most-used visual asset in any app above the simplest utility. Done well, it's invisible — users navigate without noticing the icons. Done badly, icons are the single most common reason an app feels confusing or amateur.

---

## Inventory first

Before designing or sourcing icons, list every concept that needs one:

- **Navigation** — tab bar items, back button, close/dismiss, menu/hamburger.
- **Actions** — share, add/create, edit, delete, save, search, filter, sort.
- **Content types** — photo, document, link, audio, video, location, calendar event.
- **States** — completed, incomplete, error, locked, starred/favorited, active/selected.
- **Categories / labels** — any repeating category that benefits from visual distinction.
- **Feedback** — loading (usually animated), success, warning, failure.
- **Settings / controls** — notification, privacy, appearance, account, billing.

A thorough inventory often reveals 30-80 distinct concepts in a moderately complex app. That's a substantial system design problem — and it's why pulling from a system library (SF Symbols, Material Icons) rather than illustrating everything custom is almost always the right call for a solo developer.

---

## The four properties of a working icon

Every icon should satisfy:

1. **Meaning** — what concept does this icon represent? Is it unambiguous in context?
2. **Silhouette** — what shape is it, and how distinct is it from every other icon in the set?
3. **Color** — does the active/inactive color distinction work? Does color reinforce meaning or just decorate?
4. **Scale tolerance** — does it read clearly at the smallest size it will appear on-device?

Test all four. The fourth fails most often in mobile — icons that look sharp in Figma at 400% zoom are muddy at 24×24pt in a tab bar.

---

## Silhouette test

Pull every icon to a single color (black on white, no detail). Can you tell them apart by shape alone?

Most amateur icon sets fail this test — icons that look distinct in color become indistinguishable in silhouette. Users in real use are parsing icons quickly, often in glare or at peripheral vision — silhouette is the strongest cue, before color.

The tab bar in particular demands strong silhouette distinctness. Five similar-shaped icons at 24pt, in a row, all gray except the selected one, are very easy to confuse.

---

## Color test

Pull every icon to grayscale. Can color-blind users distinguish them? Approximately 8% of men have some form of color vision deficiency (deuteranopia, red-green, is most common).

Designs that rely on red vs. green color alone — e.g., a "success" icon and an "error" icon that are identical in shape but different only in color — fail for a significant portion of users. Add shape or text as a redundant signal.

iOS and Android both offer accessibility tools to simulate color vision deficiencies. Test against them.

---

## Scale test

Render every icon at its smallest actual on-device size. For mobile, common sizes are:

| Context | Typical visual size |
|---------|-------------------|
| Tab bar | 24–28pt |
| Navigation bar action | 22–25pt |
| List row leading icon | 20–24pt |
| Contextual action in a cell | 18–22pt |
| Inline in text | 14–18pt |
| App icon (home screen) | 60×60pt |
| App icon (Spotlight / notification) | 20×20pt |

A common failure: icons designed at 48pt in Figma, exported, then rendered at 22pt on a list row — all the detail disappears. Design icon at the minimum size it will appear; then verify it still reads.

---

## Touch targets: separate from icon size

The visual icon size and the touch target size are different things. This is the most common mobile iconography mistake.

**Minimum touch target sizes:**
- **iOS (Apple HIG)**: 44×44pt
- **Android (Material Design)**: 48×48dp

An icon that is 24pt visually needs 10pt of invisible tap-area padding around it to meet the minimum. This is implemented in code (larger hit area with the same visual) — but it must be specified.

Undersized touch targets are a consistent source of user frustration and 1-star reviews: "I kept tapping the wrong button." They are also an accessibility issue; iOS and Android both evaluate touch target size in accessibility audits.

---

## System icon libraries vs. custom icons

The first decision in any mobile icon system: do you use system icons (SF Symbols on iOS, Material Symbols on Android) or design custom icons?

### SF Symbols (iOS)

SF Symbols is Apple's icon library — over 5,000 symbols, vector, integrated with the San Francisco type system, and designed to work at every weight, scale, and size class.

**Use SF Symbols when**:
- The concept is a standard iOS/system concept (navigation, actions, settings, system states).
- You want icons that feel native and immediately familiar to iOS users.
- You're a solo developer without a designer — SF Symbols is the fastest path to a consistent, professional icon system.
- You need variable weight (regular, medium, semibold, bold) and size to match your typography.

**Don't use SF Symbols when**:
- The concept is domain-specific and there's no matching symbol (e.g., your app's proprietary feature categories).
- You want a strongly branded icon style that should feel distinct from system apps.
- You're building cross-platform and need icon parity with Android.

**SF Symbols version awareness**: not all symbols are available on all iOS versions. Check minimum deployment target against symbol availability in the SF Symbols app.

### Material Symbols / Material Icons (Android)

Google's equivalent — the Material Symbols library has 2,500+ icons in outlined, filled, rounded, and sharp variants, with variable font axes (weight, fill, grade, optical size).

**Use Material Symbols when**:
- Building on Android or cross-platform with a Material Design foundation.
- You want icons that feel native to Android users.
- You need filled vs. outlined state variants (common pattern: unfilled in unselected state, filled in selected state — for tab bars especially).

### Custom icons

Custom icons are appropriate when:
- Your app has domain-specific concepts with no system equivalent.
- You have a strong brand identity that requires a distinct icon style (custom weight, rounded vs. sharp corners, custom metaphors).
- You've shipped the core product and are investing in visual differentiation.

For a solo developer in early stages, custom icons are almost always premature. Use system icons as a foundation; add custom icons for domain-specific concepts only.

**If you commission custom icons**:
- Brief to match the specific visual style (stroke weight, corner radius, metaphor style) of your chosen system library, so custom and system icons can coexist.
- Deliver as SVG (vector). Never as PNG unless the system requires it.
- Test at every size in the inventory list above before approving.

---

## Platform consistency vs. brand consistency

A persistent tension: should icons follow platform conventions closely (instantly familiar but potentially generic) or be fully custom (distinctive but with a learning cost)?

**Rule of thumb**:
- **Core navigation and system actions** (back, close, share, settings, search) → follow platform convention. Users have deep muscle memory. Deviating costs goodwill.
- **Domain-specific features** (your app's categories, custom actions, unique concepts) → custom icons are appropriate and expected.
- **Tab bar items** → if the concept maps to a SF Symbol or Material Icon, use it. Users recognize "house = home," "magnifying glass = search," "person = profile." Re-metaphoring these forces relearning.

The hybrid approach: system library as the base, custom icons layered in for domain-specific concepts, all matched in visual weight and corner radius so the set reads as unified.

---

## Iconographic grammar

Icons don't exist in isolation. You need a grammar — consistent rules for how icons combine with other elements.

Common patterns:
- **Badge + icon**: a numeric badge on a tab bar icon for notification count. Position: top-right corner. Size: follows platform convention (iOS UIKit handles automatically).
- **Icon + label**: when icons appear with text labels (tab bar, contextual menus), label positioning, font size, and active/inactive state treatment must be consistent.
- **Color for state**: inactive icons in neutral color (text-tertiary); selected/active in primary or brand color. Don't invent a third color scheme for icons.
- **Filled vs. outlined**: filled for selected state, outlined for unselected — most common tab bar convention on both platforms. Be consistent.
- **Size in context**: icons that appear next to text (e.g., in a list row) should be visually sized to sit on the cap-height of the adjacent text, not centered on the full line-height.

Pick a grammar and apply it consistently across all surfaces: tab bars, navigation bars, action sheets, list rows, buttons, empty states.

---

## Common iconography mistakes

- **Mixing icon styles.** Some icons from SF Symbols, some custom outlined, some custom filled. Pick a single family and stick to it. Mixed styles signal an unfinished product.
- **Icons that require the label to be understood.** If removing the label makes an icon incomprehensible, the icon isn't working. Test in a tab bar by hiding all labels.
- **Touch targets not specified.** The icon is small; the designer assumed the developer would know to add padding. The developer didn't. Every icon that a user taps needs a documented touch area.
- **Color as the only state signal.** Active tab icon is blue; inactive is gray. Works for non-color-blind users; fails for ~8% of male users. Add weight, fill, or size change as a secondary signal.
- **Icons that look like the competitor.** Using the same SF Symbol as a competitor's flagship feature in the same color creates confusion. If you're in the same category, audit your icon choices against the top 5 apps.
- **Animated icons with no reduced-motion fallback.** Users with vestibular disorders or motion sensitivity have iOS/Android's "Reduce Motion" setting enabled. Animated icons that don't respect this setting create accessibility issues.

---

## Quick test: the cold reader

Show your icon set to someone who hasn't used the app. For each icon in the tab bar or navigation:

- "What do you think this does?"
- "Which of these would you tap to find your account settings?"
- "Which two of these feel most similar to you?"

If core navigation icons aren't correctly identified within a second or two, redesign before building. Users in real use have less attention than a cold reader, not more.

---

## Tools and resources

- **SF Symbols app** (free from Apple) — browse, search, and copy symbol names; check availability by iOS version.
- **Material Symbols** — available at fonts.google.com/icons; variable font download for Figma.
- **Phosphor Icons** — a well-designed, consistent icon set for cross-platform use. CC-licensed with commercial options.
- **Heroicons** — Tailwind project; clean, consistent, good for web and React Native.
- **Figma component libraries** — SF Symbols and Material Icons are both available as community Figma libraries; import and use directly.
- **Vector mandatory**: all custom icons must be SVG. Bitmap icons cannot be re-used at multiple sizes cleanly.
