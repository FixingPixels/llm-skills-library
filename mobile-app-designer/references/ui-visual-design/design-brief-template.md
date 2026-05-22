# Design Brief Template

Use one brief per deliverable. Reuse this structure for app icons, key screens, design system components, onboarding illustrations, App Store screenshots, and marketing assets.

## Brief structure

```
PROJECT: [App Name]
PIECE: [What this is — App Icon, Home Screen, Onboarding Screen 2, Design System Color Tokens, etc.]
DESIGNER: [Name]
DUE: [Date]
USE / DIMENSIONS: [Where this will appear and at what size — e.g., "App icon at 1024×1024px for App Store submission; also needs @3x, @2x, @1x exports"]
BUDGET: [Agreed fee or rate]

----

PURPOSE
[1-3 sentences. What this deliverable needs to do for the product. Drive installs / communicate the
core job / enable navigation / carry brand identity through the onboarding flow.]

PRODUCT CONTEXT
[1-2 paragraphs. Who the user is, what job they're doing in the app, and why this deliverable
matters in that context. Tell the designer what they need to know — not the entire product brief.]

SCREEN / COMPONENT SPEC
[What exactly to design. Be specific about the state being shown, the content, the interactions
if relevant, and the hierarchy — what's most important visually.]

EXAMPLE:
"Home screen, logged-in state, user has 3 habits tracked. Shows a summary card at top (today's
completion), a list of today's habits with tap targets to mark complete, and a floating '+' action
button. The completion ring / summary is the visual hero. The list is secondary. Primary CTA is
marking habits complete — not creating new ones."

MOOD & TONE
[Two or three adjectives. "Calm, precise, airy." "Energetic, bold, direct." Avoid "clean" and
"modern" — meaningless without reference.]

DESIGN REFERENCES
[At least three reference apps or screens, each tagged with what to take from them.]

- [App 1 / screenshot link]: take the color balance — the warm neutrals against the teal accent.
- [App 2 / screenshot link]: take the typography hierarchy — bold heading, tight sub-label.
- [App 3 / screenshot link]: take the empty state illustration style — flat, friendly, one focal object.

DON'T
[Anti-references — what not to do. Critical for staying out of common pitfalls.]

- Don't use gradients — the design system is flat color only.
- Don't center-align body text.
- Don't use any iconography that resembles [competitor app] — we need visual distinction.
- Don't include stock photography or photo-based elements.

DELIVERABLES
- [Explorations / direction options] — by [date] — [e.g., 2-3 low-fi directions in Figma]
- [Refined direction] — by [date]
- [Final Figma file with components] — by [date]
- [Exported assets] — [specify format: PNG @1x/@2x/@3x, SVG, PDF]
- [Dark mode variants] — yes/no, if yes specify separately

LICENSE / USAGE
[How will the work be used — app UI, marketing, App Store listing, social, future expansion to
other platforms. State plainly. Match what's in the contract.]

CREDIT
[How the designer will be credited — in the app's About screen, in the App Store listing, on
your website/socials. State plainly.]
```

---

## What separates a strong brief from a weak one

**Weak**:
> Need a home screen design. Something clean and modern. Think minimal productivity app.

**Strong**:
> Home screen for a daily habit tracker. Target user: adults who want a low-commitment daily routine. State shown: user has 3 habits, has completed 1 today (morning workout). Visual hero: a completion ring showing 33% progress. Below that: a list of today's 3 habits — each with an icon, a name, and a tap-to-complete checkmark. Floating '+' button bottom-right for creating new habits.
>
> Tone: calm and focused — the design should feel like opening a clean notebook, not launching a productivity machine.
>
> References: spacing and typography from Bear (notes app); habit ring from Streaks; list density from Things 3.
>
> Don't: use gamification elements (no XP, no badges, no confetti animations); don't make the completion percentage the headline number — it's supporting context, not the hero.
>
> Deliverables: Figma frame with auto-layout components, @3x exported PNG, dark mode variant.

The difference is specificity, a named hierarchy, anti-references, and a clear spec of the exact state being designed.

---

## When the designer comes back with the wrong direction

Sometimes the first pass misses. Diagnose before redirecting:

- Did your **brief** specify the wrong thing? Often the brief said "minimal" when you meant "airy with clear structure." Look at the brief with fresh eyes.
- Did the designer **misread** the brief? Look at where they diverged — that's a clue about what was unclear or ambiguous.
- Did the designer follow the brief but the brief was **wrong about the product**? You may have misdescribed what the screen needs to do.

Don't ask for full redesigns if you can help it. Smaller, specific asks ("can the CTA button sit lower — above the tab bar, not center screen?" or "the font weight on the habit names needs to be lighter — they're competing with the heading") cost the designer less and keep the scope clean.

The rule: ask for composition and hierarchy changes early (exploration stage), ask for color and typography refinements in the second pass, ask for polish-level changes (spacing, corner radius, shadow) last.

---

## Brief volume and pacing

An app with 15 distinct screens might need 15 briefs plus icon briefs plus marketing asset briefs. That's a lot. Strategies:

- **Tier the briefs.** App icon gets a full brief. Key screens (home, onboarding screen 1, paywall) get full briefs. Secondary screens might get a 5-line brief that references the design system established in the primary briefs.
- **Brief the design system once**, then per-screen briefs inherit it.
- **Group similar screens.** Five list-pattern screens can share a template brief; five form screens can share another.
- **Iterate in batches.** Get explorations for 3 screens before finalizing any, so you can correct direction early and apply it across the batch.

---

## App Store asset briefs

App Store screenshots are a distinct deliverable — they are marketing assets first, UI screenshots second.

Screenshot brief structure:

```
PIECE: App Store Screenshots (set of 6) — iPhone 6.5" size
PURPOSE: Convert a visitor in the App Store who has never heard of the app into an install.
         Screenshots are the primary pitch. They must communicate value, not just show UI.

SPEC PER SCREENSHOT:
  Screenshot 1: Hero value prop
    - Headline text: "[Core benefit — e.g., 'Track your mood in under 10 seconds']"
    - Visual: [Describe which screen / what state / any surrounding device frame or context]
    - Background: [Solid color / gradient / pattern — specify hex or describe]

  Screenshot 2: Primary feature in use
    - [As above]

  Screenshots 3-6: [Brief for each]

STYLE: [Should match app visual language or may be distinct marketing style — specify]
DELIVERABLES: PNG at 1290×2796px (iPhone 6.5" @3x), also 1242×2688px if targeting older size class
DON'T: Show loading states, error states, or empty states. Every screenshot should show the best
       possible populated state.
```

---

## Design system brief (for initial build)

When the brief is for the design system itself rather than a specific screen:

```
PIECE: Design System — Color, Typography, Component Library
PURPOSE: Establish the visual language the entire app will be built on. All future screens and
         components should be derivable from this system.

SCOPE:
  Colors: Primary, secondary, accent, neutral scale (8 steps), semantic colors (error, warning,
          success, info), background/surface levels (3-4 levels), text levels (3-4 levels).
          Light mode and dark mode versions of all.

  Typography: Scale (display, heading 1-3, body large/regular/small, label, caption).
              Font family / families. Weights used. Line heights. Letter spacing.

  Spacing: Base unit (typically 4pt or 8pt). Named scale (xs, sm, md, lg, xl, 2xl).

  Radius: Named scale (sm for inputs, md for cards, lg for sheets, pill for buttons/tags).

  Elevation/shadow: 3-4 shadow levels for iOS / elevation levels for Android.

  Components: [List core components needed — Button (primary, secondary, destructive, ghost),
              Input field, Card, List row, Tab bar item, Navigation bar, Modal sheet, Empty state]

DELIVERABLES: Figma library file with styles and components; light and dark mode; all components
              with variants (default, hover/pressed, disabled, loading); annotated with token names.
```
