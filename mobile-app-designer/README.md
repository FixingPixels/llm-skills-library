# mobile-app-designer

A design partner that takes you from "I have an idea for an app" all the way to production-ready screens. It's read the iOS Human Interface Guidelines and Material Design specs so you don't have to, and it knows how to pressure-test an idea before you build the wrong thing.

## Who it's for

Solo founders, indie developers, and small teams shipping mobile apps without a dedicated designer — or with one who's overloaded.

That includes people at very different stages: you might have a rough idea and want to know if it's worth designing, or you might have a Figma file and want a platform-convention check before you hand it to an engineer. Both are valid starting points.

## What it does

Works across the full span from concept to screen:

**Idea stage** — before a pixel exists
- Turn a rough concept into a concrete problem statement and target user
- Map out the core user journey and the one thing the app must nail
- Identify assumptions worth testing before you build
- Suggest the minimum set of screens to validate the idea

**Design and review** — once you're building

Designs and reviews mobile UI with the constraints that actually matter on a phone:

- Onboarding flows, settings screens, empty states, paywalls, error states
- Platform-correct patterns — when to use a sheet vs a modal, tab bar vs navigation rail, system back vs custom back
- Thumb-zone and reachability checks for one-handed use
- Touch target sizing (44pt iOS, 48dp Android) and spacing
- Dynamic Type and font scaling, dark mode parity, safe-area handling
- Accessibility: VoiceOver and TalkBack labels, contrast ratios, motion reduction
- App Store and Play Store screenshot specs and review guidelines
- UX copy for buttons, alerts, permissions prompts, and empty states

## Trigger examples

Starting from an idea:
- "I want to build an app that helps people track their water intake — where do I start?"
- "Is this app idea worth designing? Here's the concept..."
- "What are the three screens I'd need to validate this idea?"
- "Help me figure out what the core loop of my app should be"

Starting from a design:
- "Design an onboarding flow for a habit tracker"
- "Review this settings screen — what am I missing?"
- "Should this be a modal, a sheet, or a full-screen takeover?"
- "Write the permission prompt copy for location access"
- "Is this accessible on iOS?"
- "What's the right empty state for a feed with no posts yet?"
- "Design a paywall that doesn't feel scammy"
- "Fix my tab bar — something's off"

## What it doesn't do

This is a mobile specialist, not a generalist. For broader work, reach for the sibling skills:

- `design:design-critique` — general design feedback across web and mobile
- `design:accessibility-review` — full WCAG audit on any surface
- `design:ux-copy` — writing microcopy without the mobile-specific framing
- `design:user-research` — research planning, not design execution

It also doesn't do brand identity, marketing site design, or backend architecture.

## Example session

> **You:** I'm building a meditation app. Need an onboarding flow.
>
> **Skill:** Three questions before I draft anything: is this iOS-only, Android-only, or both? Do you want to collect any info upfront (name, goals, experience level), or get the user into the app as fast as possible? And do you have a paywall — if so, does it appear during onboarding or after first use?
>
> **You:** iOS first. Get them in fast. Paywall after day 3.
>
> **Skill:** Then I'd keep onboarding to three screens: value prop, permissions ask (notifications, with a soft pre-prompt), and a one-tap first session. Here's the flow with copy, layout notes, and the system pattern for each screen...

## Installation

Install through the Cowork plugin manager or add to your `skills/` directory.

## Feedback

This skill is opinionated about mobile conventions. If it tells you something is wrong on iOS and you disagree, push back — it'll cite the HIG section or explain its reasoning. If it's actually wrong, file an issue.