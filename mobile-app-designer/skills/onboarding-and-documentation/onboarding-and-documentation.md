---
name: onboarding-and-documentation
description: >-
  This skill should be used when the user is writing, designing, or fixing an onboarding flow,
  first-launch experience, in-app help content, App Store listing, or release notes. Trigger on:
  "onboarding flow", "first launch", "App Store description", "screenshots", "empty state",
  "coach marks", "tooltips", "permission prompts", "sign-up flow", "user doesn't know how to",
  "help content", "release notes", or any documentation and first-experience question.
---

# Onboarding and Documentation

Help a solo indie developer or non-technical founder turn a working app into a **first-launch experience** that strangers can pick up, understand, and get value from — without the developer in the room.

This is the most underestimated skill in mobile development. A great app with a bad onboarding will get deleted in the first session, generate "I don't get it" reviews, and churn users before they ever reach the feature that makes the app worth keeping. A merely good app with excellent onboarding will retain, convert, and grow.

Most users will never read documentation. The onboarding *is* the manual. There is no backup plan.

## Operating mode: Socratic, but a craft

Onboarding has conventions the way rulebooks have conventions. The coaching voice still applies — ask before prescribing — but good onboarding is a real craft with real patterns. Don't reinvent the wheel.

When a user brings a flow or draft, the first move is questions:

- Who's the target user? (First-time user vs. converting from a competitor.)
- Has the app been tested with real users outside the developer's network?
- What's currently failing — are users not activating, not converting, not returning?
- Is the onboarding the problem, or is the core loop unclear? (Onboarding can't fix a product people don't want.)

If the app hasn't been tested by real users, name that. You can help draft onboarding, but it can't be finalized until real users have tried it.

## The two users of an onboarding flow

Every onboarding decision must work for two users:

1. **The first-time user**, encountering the app cold, with no context.
2. **The returning user**, coming back after days or weeks away, trying to remember how something works.

Optimize the first-launch flow for the first-time user — simple, value-forward, minimal friction. Optimize for the returning user with in-app help, contextual tooltips, and a clear navigation structure that doesn't require memorization.

If a feature is so complex that users can't remember how it works after a break, that's a UX problem, not a help-content problem.

## Teach flow vs. reference flow

These are different. The first-launch flow is about *activation* — getting the user to their first "aha" moment. In-app help is about *reference* — answering questions when the user has a specific problem.

A well-designed first-launch flow should:
1. State the core value immediately. ("This app does X for you.")
2. Show, not tell — get the user doing the primary action within 60 seconds.
3. Defer every secondary feature and permission ask until after the user has experienced value.
4. End with a clear "what to do next," not a blank canvas.

Concrete reference points: **Duolingo** drops the user into a real lesson within 90 seconds, before account creation. **Streaks** puts the "add your first habit" action front-and-center on a single screen. **Day One** opens to a write prompt, not a tour.

A well-designed reference structure should:
- Be findable from the screen where the user has the problem.
- Answer the specific question, not give a tour of all features.
- Link to related help from within the answer.

## The canonical first-launch flow order

There are stylistic variations, but the canonical structure for a well-designed mobile onboarding is:

1. **App icon and splash** — fast, branded, no bloat. Loads the app, not a slideshow.
2. **Value proposition screen(s)** — 1-3 screens maximum. What this app does and why it matters. Visual, not text-heavy.
3. **Sign-up / sign-in decision** — offer "continue without account" if at all possible. Every sign-up wall before value is a leak. If account creation is required, make the reason clear.
4. **Personalization (if needed)** — only ask for what shapes the first experience. Every question that doesn't change what the user sees next is friction.
5. **Core action** — get the user to perform the primary action of the app. Not a demo, not a tutorial animation — actual use.
6. **Value confirmation** — reinforce that something happened. The user did the thing; show them the result.
7. **Permission asks** — after value, not before. Push notifications especially. (See permission ask sequencing below.)
8. **Home / core loop** — the user is now in the app. The first empty state or populated state sets up every future session.

For a full scaffold, see [onboarding-flow-template.md](../../references/onboarding-and-documentation/onboarding-flow-template.md).

## Permission ask sequencing

Permission requests are the most dangerous friction point in an onboarding flow. Getting them wrong is irreversible — a user who denies a permission rarely goes back to grant it.

**The rule**: ask for a permission at the moment the user will understand exactly why it's needed and have just experienced the reason it makes their life better.

- **Push notifications** — ask after the user has completed a meaningful action and seen a result. Never on first launch. The ask should explain what kind of notification: "We'll remind you to log your daily mood." Not "Allow Notifications."
- **Location** — ask at the moment the user triggers a location-dependent feature, not during setup. Include a purpose string that explains the specific use.
- **Camera / microphone** — ask at the exact moment the user taps the camera or mic button. Not before.
- **Contacts / health / motion** — ask when the feature is accessed, with a clear value statement and "you can do this later" option.
- **Tracking (App Tracking Transparency, iOS)** — ask after onboarding. Include a custom pre-prompt that explains why it makes the user's experience better; the system prompt alone has terrible conversion.

**Never** front-load multiple permission asks on a cold screen. A user who has just installed the app and immediately sees "Allow Notifications, Allow Location, Allow Contacts" — all on separate system sheets — will deny all of them and assume the app is collecting data inappropriately.

## Empty states: the most neglected screen

The first empty state is the first honest test of whether the app teaches itself. When a user has no data, no history, no content — what do they see?

Bad empty states:
- A blank screen.
- A generic illustration with "Nothing here yet."
- A long paragraph explaining the feature.

Good empty states:
- A clear call to action: one button, one job. "Create your first habit →"
- A short, specific explanation of what this section will contain when populated.
- A sample or example that shows what the filled state will look like. (Especially for data-visualization or tracking features — show a fictional example chart.)
- For collaborative or social features: suggest invite actions or ways to find others.

Concrete reference: **Things 3** shows a sample to-do in its empty Today list; **Strava** uses an example route preview on a first-time activity feed.

## Tooltips and coach marks

Use sparingly. When onboarding requires tooltips to explain a feature, the feature itself may be unclear.

**Tooltips** (appear on hover/long-press or in a help section):
- For labels that need a single-sentence explanation.
- Context-specific, dismissible, non-blocking.
- Don't use for critical path actions — those must be self-evident.

**Coach marks** (spotlight or callout overlays on first use):
- One at a time. Never stack coach marks.
- Only for gestures or interactions that can't be inferred from the UI (e.g., a swipe-to-reveal action).
- Dismissible immediately. Never trap the user in a mandatory tutorial that can't be skipped.
- Show on the first relevant interaction, not on every cold launch.

## App Store listing as onboarding surface

The App Store listing is the first screen your user sees. Most won't install without reading at least the icon, name, screenshots, and first sentence of the description.

**Hierarchy of importance** (what users actually see before the fold):
1. **App icon** — quality signal; must read at small sizes.
2. **App name + subtitle** — should state the primary use case; these are also keyword-indexed.
3. **Screenshots / preview video** — the real pitch. First screenshot should state the core value, not show the UI for its own sake. ("Write 200 words every morning." Not a UI screenshot with no context.)
4. **Ratings and review count** — apps below 4.0 stars have a significant conversion penalty.
5. **First sentence of the description** — this is visible before "more." Make it the value proposition.

For writing the App Store listing and localizing the copy, see [onboarding-flow-template.md](../../references/onboarding-and-documentation/onboarding-flow-template.md).

## Voice in onboarding copy

Onboarding has multiple distinct writing registers. Mixing them produces copy that feels off.

For voice guidance on instructional copy, brand voice, and release notes, see [voice-and-tone.md](../../references/onboarding-and-documentation/voice-and-tone.md).

## The one-hour onboarding copy review

When a user has a draft onboarding and wants a tightening pass:

1. **Find every screen that has more than two sentences of explanation.** The explanation is revealing a design problem; reduce or move to help content.
2. **Find every passive sentence in button labels and actions.** "Submit" → "Save journal entry." "OK" → "Got it." Passive, generic labels erode trust.
3. **Find every permission ask and check its placement.** Is each ask preceded by a moment of value? Is the purpose string specific?
4. **Check every empty state.** Does it contain a clear action? A sample of what filled looks like?
5. **Read every onboarding screen aloud.** Awkward phrasing shows up in reading.
6. **Find every place where the app says "you can" instead of just doing it.** "You can tap the + button to add a habit" → show a coach mark the first time, or redesign so it's discoverable.
7. **Check the App Store listing screenshots.** Does screenshot 1 state the value, not just show the UI?
8. **Verify notification permission timing.** Is the ask after the user has seen value?

## Common onboarding failures

When user tests show drop-off, activation failure, or negative reviews mentioning confusion, run through these:

- **User doesn't understand what the app does after 30 seconds** — the value prop screen is absent or too abstract.
- **Sign-up wall before value** — users who hit account creation before experiencing the app's core value have high abandonment. Defer or offer a guest mode.
- **Too many onboarding screens** — aim for the minimum to reach the first core action. Three screens is a ceiling for most apps; five is usually too many.
- **Permissions asked cold** — any system permission asked on a blank screen before the user has done anything will be denied at high rates.
- **Empty state paralysis** — user reaches the home screen and doesn't know what to do first. The first CTA must be unmissable.
- **Paywall before value** — showing a subscription paywall before the user has experienced the benefit they're being asked to pay for. Especially damaging in the first session.

For a complete diagnostic guide, see [common-onboarding-failures.md](../../references/onboarding-and-documentation/common-onboarding-failures.md).

## Help content and release notes

Beyond the first-launch flow:

- **In-app help** — a searchable FAQ or support section reachable from the settings or any screen where confusion occurs. The bar is: a user who is confused about X should be able to find the answer in under 30 seconds.
- **Contextual help** — a "?" icon or tooltip on any UI element where the purpose isn't self-evident. Small investment, high trust return.
- **Release notes** — the changelog copy in each App Store update. Most developers write "Bug fixes and performance improvements." The ones who write specific, honest release notes build user loyalty and get featured more often. **Overcast** and **Carrot Weather** are the standard references here — short, specific, written by a human. See [voice-and-tone.md](../../references/onboarding-and-documentation/voice-and-tone.md) for the designer/release notes voice.

## What to avoid

- **Don't finalize onboarding before testing with real users.** Untested flows have unknown drop-off points. What makes sense to the developer is often invisible to a first-time user.
- **Don't use onboarding to compensate for an unclear product.** If the core loop requires 10 screens to explain, the core loop needs redesign, not a better tutorial.
- **Don't front-load permissions.** Permission denial is irreversible. Sequence every ask for maximum context and minimum surprise.
- **Don't skip the empty state.** The blank screen is where engagement goes to die.
- **Don't write "Bug fixes and improvements" in release notes.** Your users are people. Talk to them.

## Handoffs

- Onboarding reveals a UX problem (a flow that can't be explained because it's genuinely confusing) → back to [ux-interaction-design](../ux-interaction-design/ux-interaction-design.md).
- The user wants the onboarding to feel more on-brand, or needs App Store screenshot design → [ui-visual-design](../ui-visual-design/ui-visual-design.md).
- The user is deciding what to show in the paywall or what to gate → [monetization-strategy](../monetization-strategy/monetization-strategy.md).

Name the handoff explicitly.
