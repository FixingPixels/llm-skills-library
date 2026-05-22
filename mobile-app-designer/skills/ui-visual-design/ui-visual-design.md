---
name: ui-visual-design
description: >-
  This skill should be used when the user is working on the visual identity of their app — app icon,
  screen layouts, design system, iconography, color and typography, component design, dark mode,
  or briefing freelance designers. Trigger on: "ui design", "visual style", "design system",
  "app icon", "screen layout", "iconography", "design brief", "moodboard", "hire a designer",
  "component design", "dark mode", "brand identity", or any visual design question.
---

# UI Visual Design

Help a solo indie developer or non-technical founder make their app **look** like itself. UI visual design covers more than picking colors — it's app icon, screen layouts, design system, typography, iconography, component aesthetics, and the brief that gets those things produced by a freelance designer or implemented by a developer.

This is where solo developers most often hit reality. Most can't produce polished visual design themselves; they need to either direct a freelancer or make thoughtful decisions within a design system (iOS HIG or Material Design) that does the heavy lifting. Bad direction wastes money and produces inconsistent screens. Good direction is the cheapest way to make a solo app look considered.

## Operating mode: Socratic, with references

Same coaching voice. But visual design is *especially* concrete — the user benefits from naming reference apps whose look they admire early and often.

When a user asks for visual design help, start with:

- What existing apps **look** how you want yours to look? Name at least three.
- What's the platform? (iOS-only, Android-only, or cross-platform — this determines the design language baseline.)
- Who is the audience? (Different audiences trust different visual languages.)
- What should a user *feel* the first time they open this app?

Without these, direction is hand-waving.

## What UI design has to do in a mobile app

Three jobs, ranked:

1. **Earn trust on first impression.** The app icon and first screen do 80% of the user's trust-formation. If the visual design signals "amateur" or "unclear what this is," users delete before they try.
2. **Make the app usable.** Screen hierarchy, touch target sizes, contrast, iconography, layout — users need to read and operate the app in real time. Bad visual design makes a fine product frustrating.
3. **Carry the brand identity.** The visual design should reinforce what the product stands for — calm, energetic, precise, playful — so the user feels in the right place from the moment the app opens.

If a visual choice doesn't do at least one of these, it's vanity. Cut it.

## Core deliverables a UI visual design process produces

For a solo developer building or briefing a designer, the process produces:

1. **Visual reference document / moodboard.** Real apps and design assets, tagged with what each contributes (color, typography, density, feel).
2. **Design system.** Color tokens, typography scale, spacing system, corner radius, shadow and elevation rules, component library.
3. **Design briefs.** Per-deliverable briefs for each screen, icon, or design system component commissioned from a freelancer.
4. **Screen and component specs.** For every screen and interactive component — sizes, safe areas, asset export formats, Figma handoff notes.
5. **App icon.** A distinct, small-size-readable mark that communicates the app's identity in 60×60 points.

For a design brief template, see [design-brief-template.md](../../references/ui-visual-design/design-brief-template.md). For a screen and component spec checklist, see [screen-and-component-specs.md](../../references/ui-visual-design/screen-and-component-specs.md).

## Visual style: starting point

Most solo developers start by describing a style vaguely ("clean," "minimal," "modern"). Push for specificity.

Useful axes:

- **Design language stance**: Platform-native (iOS HIG / Material Design) | Brand-custom | Hybrid (platform structure with custom brand layer)
- **Density**: Information-dense (many elements per screen) | Airy (generous whitespace, few elements)
- **Color approach**: Monochromatic | Limited palette | Full brand palette | System-adaptive (follows OS dark/light)
- **Typography personality**: System fonts (San Francisco, Roboto) | Custom font | Serif editorial | Display fonts for headings
- **Illustration presence**: Icon-only | Spot illustrations | Full illustration style | Photography | Abstract / geometric
- **Tone**: Warm | Cool | Neutral | Playful | Serious | Premium | Approachable

Get the user to commit to a phrase: "Airy, brand-custom with iOS structural conventions, warm neutral palette, system typography." That's a direction a designer can execute. "Clean and modern" is not.

For more reference patterns, see [mobile-design-language-references.md](../../references/ui-visual-design/mobile-design-language-references.md).

## The app icon: the highest-stakes single asset

The app icon is the smallest, most-seen piece of visual design in the product. It appears at:
- 60×60pt (iPhone home screen) — the primary context
- 20×20pt (Spotlight, notifications) — must read as a distinct shape
- 1024×1024pt (App Store listing) — must look polished at large scale
- Contextual sizes in iOS settings, notification center, share sheets

Good app icons:
- **Read as a distinct silhouette.** From the home screen, surrounded by 20 other icons, does it have a recognizable shape? Most icons fail this.
- **Communicate the core job or personality.** The icon is the brand. What does it signal?
- **Work in both light and dark contexts.** iOS puts icons on both light and dark wallpapers; Android adaptive icons have background and foreground layers.
- **Are not logotype.** A word mark at 60×60pt is illegible. Icons should be shapes, not text.

Concrete references to study: **Things 3** (single curved checkmark, instantly readable at any size), **Bear** (one shape that doubles as a bear and a writing app), **Procreate** (a single paintbrush stroke that signals the entire product). All three pass the silhouette test from across the room.

Bad app icon patterns: stock iconography in a colored square; the app name as the icon; too-detailed artwork that disappears at small sizes; a literal representation of the most generic aspect of the app.

## Iconography: the unsung hero

In any app above the simplest utility, **iconography carries the load** of navigation and action legibility. Good iconography is invisible — users navigate without noticing the icons. Bad iconography makes a well-designed app confusing.

For a workable mobile iconography system, see [mobile-iconography.md](../../references/ui-visual-design/mobile-iconography.md).

Core principles here:
- **One concept per icon.** A "settings" icon means settings, everywhere.
- **Visual distinction at touch scale.** Test at 24×24pt (the smallest common tab bar icon size), not at design-tool zoom.
- **Platform conventions are strong.** Don't reinvent well-established icons (back chevron, share sheet, heart/like, magnifying glass search). Users have muscle memory.
- **Touch targets are separate from visual icon size.** An icon can be 24pt visually while having a 44×44pt touch area.

## Screen layout: the most-used surface

Every screen is read by users making fast, low-attention decisions. Layout problems multiply across thousands of sessions.

Layout principles for mobile:
- **One primary action per screen.** The hierarchy should make one action obviously more important than others. When everything is equal, nothing is.
- **Thumb zone awareness.** On a standard iPhone, the natural thumb reach covers roughly the bottom 40-50% of the screen. Primary actions and interactive elements belong there. Destructive or rare actions can be out of easy reach.
- **Visual hierarchy mirrors information priority.** The most important information should be largest, highest-contrast, highest on the screen.
- **Content, not chrome.** Navigation bars, tab bars, and status bars should be minimal — the content is why the user is here.
- **Platform standards reduce cognitive load.** Navigation patterns users already know (tab bar at the bottom on iOS, floating action button on Android, swipe-back) cost zero learning. Deviating costs learning budget the user may not spend.

## Working with freelance designers

If the user is hiring a designer (which most paths to polished mobile UI require), practical rules:

- **Brief specifically.** Vague briefs produce vague work. Provide reference apps, annotated screenshots, and what *not* to do.
- **Give product context.** The designer needs to know who the user is, what job they're doing, and why this screen matters in the flow.
- **Ask for explorations first.** 2-3 directions as low-fidelity mockups before committing to one. Catching a direction problem at exploration stage is cheap; at final handoff it's expensive.
- **Iterate in passes.** Direction → wireframe → visual design → polished screens. Don't ask for pixel-perfect changes at the wireframe stage or conceptual changes at the polished stage.
- **Specify what you need delivered.** Figma frames, exported assets at @1x/@2x/@3x, component variants, dark mode versions. Vague "final files" agreements produce incomplete handoffs.
- **One designer where possible.** Multiple designers rarely produce a unified visual language without strong direction. A single consistent design voice is harder to achieve across a team.

For design brief structure, see [design-brief-template.md](../../references/ui-visual-design/design-brief-template.md).

## The platform-native vs. custom design decision

This is the most important upfront decision in mobile visual design, and most solo developers get it wrong.

**Platform-native (follow iOS HIG or Material Design closely)**:
- Faster to build (system components are free).
- Users already know how to use it.
- Passes App Store review more easily.
- Limited brand differentiation.
- Best for: utility apps, productivity tools, apps in competitive categories where usability matters more than brand.

**Brand-custom design**:
- More distinctive, more memorable.
- Higher build cost (custom components, more edge cases).
- More risk (non-standard interactions cost user learning).
- Best for: apps where the experience *is* the differentiator; apps with strong brand identity; consumer lifestyle apps where the visual feel creates retention.

**Hybrid (platform structure, custom brand layer)**:
- The most common effective approach for solo developers.
- Use system navigation, system components, system typography scale — but add a custom color palette, custom accent shapes, custom empty states and illustrations.
- Result: feels native and fast, but looks owned.

Most well-regarded indie apps use the hybrid approach: they feel like iOS or Android, but they don't look like every other app. **Things 3**, **Bear**, and **Overcast** all sit here — system structure, distinctive surface.

## Dark mode

Dark mode is no longer optional on iOS or Android. It's an OS-level feature that users control.

Design implications:
- **Don't just invert the light mode.** Dark mode needs its own color tokens. True black (#000000) backgrounds cause eye strain; most platforms use elevated dark grays.
- **Elevation is expressed differently in dark mode.** On iOS, lighter surfaces appear higher. On Android Material, surfaces gain slight lightening as they stack.
- **Image and illustration handling.** Photos often look better in dark mode with a slight vignette or border. Flat illustrations designed for light mode may look oversaturated.
- **Test both modes together.** Users switch frequently. Inconsistency between modes destroys the sense of a polished product.

## What to avoid

- **Don't start with "what color scheme?"** Start with the experience the user should have. Visual choices follow.
- **Don't direct without references.** Verbal-only direction produces inconsistent screens. Pull at least three specific apps per major visual direction decision.
- **Don't ignore the app icon.** It's the brand. Spending days on screen design and one hour on the icon is backwards.
- **Don't underweight iconography.** It's unglamorous work, but it's where apps succeed or fail during navigation.
- **Don't skip dark mode.** It's expected on both platforms. Designing light-only and "adding dark mode later" produces a worse dark mode every time.
- **Don't over-customize core navigation patterns.** The bottom tab bar, the swipe-back gesture, the standard modal — users have built-in expectations. Breaking them costs learning budget and produces negative reviews.

## Handoffs

- Visuals are revealing an unclear product identity (can't decide what the app should feel like because the positioning is unclear) → back to [product-ideation](../product-ideation/product-ideation.md) or [market-research](../market-research/market-research.md).
- The user wants iconography to match the App Store listing and onboarding screens → coordinate with [onboarding-and-documentation](../onboarding-and-documentation/onboarding-and-documentation.md) (visual consistency across listing and in-app must be maintained).
- The user wants to position visually for a market gap → [market-research](../market-research/market-research.md).

Name the handoff explicitly.
