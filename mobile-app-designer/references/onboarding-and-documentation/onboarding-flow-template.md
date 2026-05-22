# Onboarding Flow Template

A working scaffold for the full onboarding and documentation ecosystem. Adjust to fit the app, but use this as the starting point. Sections are ordered from first-user-touchpoint to long-term documentation.

---

## App Store listing

The listing is the first onboarding surface — before the app is installed.

### App icon

```
[ICON]

Reads clearly at 60×60pt (iPhone home screen) and 20×20pt (Spotlight search).
Works in both light and dark contexts.
Not a logo dump — should convey the core job or feeling at a glance.
```

### App name + subtitle

```
[App Name]               ← Primary keyword field. Max 30 characters.
[Subtitle]               ← Secondary keyword field. Describes the job. Max 30 characters.

Example: "Oak — Breathing & Meditation" / "Guided breathwork for calm"
```

### Screenshots (6 allowed; first 3 are most important)

```
Screenshot 1: Core value statement
  - Headline at top or bottom of the screenshot
  - Single sentence: what this app does for you
  - NOT a raw UI screenshot — branded, with context copy

Screenshot 2: Primary feature in action
  - Show the main interaction the user will do most
  - Annotated or headlined

Screenshot 3: Secondary feature or differentiator
  - The thing that makes this app worth choosing over alternatives

Screenshots 4-6: Supporting features, social proof, awards
```

### Preview video (optional but high-converting)

```
- 15-30 seconds maximum
- Show the core loop happening, not a marketing montage
- No voiceover required; works muted (most users have sound off)
- First 3 seconds must communicate the value — users decide immediately
```

### Description

```
[First sentence — visible before "More"] 
← This is the value proposition. Must work standalone.
← "Track your mood in under 10 seconds, every day."

[First paragraph — what the app does and who it's for]
[Second paragraph — key features, benefit-framed]
[Third paragraph — social proof, notable reviews, press, or awards if any]

[Feature list — bullet points, benefit-first]
• Track your mood with a single tap
• See patterns across weeks and months
• Export your data anytime

[Closing CTA — optional]
"Start your free 7-day trial."
```

### Keyword field (iOS only)

```
100 characters total. Comma-separated. No spaces.
Do NOT repeat words already in title or subtitle.
Use synonyms, adjacent jobs, and category terms.
Example: "journal,diary,mental health,wellness,anxiety,stress,check-in,reflect,emotion"
```

---

## First-launch flow scaffold

Design each screen as a distinct deliverable. Every screen has one job.

### Screen 0: Splash / loading

```
- App icon, centered
- Brand color background
- No copy, no marketing
- Loads as fast as possible — this is not an opportunity for a message
- Target: under 1.5 seconds on a mid-range device
```

### Screen 1-3: Value proposition

```
Screen 1:
  Headline: [Core benefit — specific, outcome-oriented]
  Visual: [Illustration or screenshot showing the outcome]
  Body: [Optional 1-sentence elaboration]

Screen 2:
  Headline: [Second benefit or key feature]
  Visual: [...]
  Body: [Optional]

Screen 3 (optional):
  Headline: [Differentiator or social proof]
  Visual: [...]
  CTA: "Get Started" or "Continue"

Navigation: dot pagination indicator. Skip button top-right from screen 1.
```

### Sign-up / sign-in screen

```
Primary: [Sign up with Apple / Sign up with Google]   ← lowest friction, recommended first
Secondary: [Sign up with email]
Tertiary: [Continue without account]   ← include if the app can function without one

Copy: Do NOT say "Create an account." Say what the account enables:
  "Save your progress and sync across devices."
  "Your data stays private and backed up."

Never: Show this screen before the value prop screens.
Never: Require an account if the app's core value doesn't require one.
```

### Personalization (if needed)

```
Rule: Only ask questions whose answers change what the user sees immediately.

Good questions:
  "What's your primary goal?" → Changes which features are surfaced first
  "How often do you want to track?" → Sets default reminder frequency
  "Which platform are you migrating from?" → Enables import flow

Bad questions (defer or remove):
  "What's your name?" → Doesn't change the experience
  "How did you hear about us?" → Analytics, not UX; move to post-activation or settings

Format: Single question per screen. Clear options. "Skip" always available.
Progress indicator visible.
```

### Core action screen

```
This is the most important screen in the onboarding flow.

Goal: Get the user to perform the primary action of the app for the first time.

Format:
  - Pre-populated or template-driven: reduce blank-canvas paralysis
  - Single CTA: "Create your first [thing]" / "Log your first [event]"
  - Framing: "Let's get you started" — active, collaborative, present tense
  - Should feel like using the app, not being taught about it

Examples by app type:
  Habit tracker → "Name your first habit"
  Journaling app → "Write your first entry" (with a prompt pre-loaded)
  Budget app → "Add your first expense" (or "Connect your bank")
  Workout app → "Start your first workout" (show a beginner routine)
  Meditation app → Immediately launch a short intro session
```

### Value confirmation / "aha moment" screen

```
After the first core action is completed:

  - Acknowledge what the user did: "Your first habit is tracked. ✓"
  - Show an immediate result: a streak of 1, a chart starting to fill, a completion animation
  - Forward momentum: "Come back tomorrow to keep your streak going."
  - This is the highest-conversion point for a permission ask or upsell — the user just got value.
```

### Permission asks (sequenced post-value)

See permission sequencing guide in the main skill file. Template for the custom pre-prompt:

```
[Permission Pre-Prompt Screen]

Icon: [Relevant illustration — not the system icon]
Headline: "[Specific benefit of granting this permission]"
Body: "[One sentence explaining exactly how it's used. No fluff.]"
  Example: "We'll send you a gentle reminder at the time you choose — nothing else."

CTA: "Continue" → triggers system permission dialog
Secondary: "Not now" → skips; can be enabled later in settings

After denial: Show a settings path:
  "You can enable this later in Settings → Notifications → [App Name]."
```

### Home screen — empty state

```
Every empty-state screen needs:

1. A clear primary action:
   Single button or prominent tap target. One job.
   Label: action-oriented ("Log your first expense", not "Add")

2. A description of what this section will contain:
   Short, specific. "Your tracked habits will appear here."
   Not: "Nothing here yet!"

3. An illustration or example (recommended):
   Show a realistic populated state as a ghost/muted example.
   Reduces anxiety about whether the user is doing it right.

4. For social or collaborative features:
   An invite or "find people" CTA alongside the create CTA.
```

---

## Notification permission timing and copy

### When to ask

```
Session 1:  After first core action + value confirmation
            OR: When the user first reaches a feature that inherently benefits from notifications
            NEVER: On first screen, before sign-up, or before core action

Session 2+: If denied in session 1, a soft re-ask in context is appropriate:
            "Want a daily reminder? Enable notifications →" (links to settings)
```

### Custom pre-prompt template

```
Illustration: [Custom branded image — not system icon]
Headline: "Stay on track with [specific reminder type]"
Body: "We'll remind you to [specific action] at [time/context]. No spam, ever."
Primary CTA: "Enable Reminders"   → triggers system dialog
Secondary CTA: "Maybe Later"      → deferred; soft re-ask after next core action

After system prompt:
  If accepted → "Great! Set your reminder time:" [time picker]
  If denied → "No problem. You can enable reminders anytime in Settings."
```

---

## Returning user experience

### Session 2 (1-3 days after install)

```
- Launch directly to the point of last progress, not the home screen
- Show a "welcome back" state only if meaningful context has changed (e.g., a streak milestone)
- Surfaceable: one new feature discovery if the core loop has been completed once
- Do NOT re-run onboarding screens; do NOT re-ask for permissions already granted
```

### Session 7 (1-2 weeks in)

```
- If the user has established a pattern: appropriate moment for a soft upsell or paywall for a
  feature they've been approaching
- If the user hasn't returned since session 1: re-engagement push notification (if permitted)
  with a specific hook: "You set up [X]. Here's what you'd have if you'd tracked every day."
- App Store review request: appropriate timing for users who have completed the core loop 3+ times
  Use SKStoreReviewRequest (iOS) — never a custom modal that blocks the UI
```

### Session 30+ (established user)

```
- Progressive feature disclosure: surface power-user features contextually, not all at once
- Changelog notes for new features are the primary onboarding for existing users
- In-app help becomes important for features the user may not have discovered
```

---

## App Store review prompt

```
When to ask:
  - After a positive action (completed a workout, finished a session, hit a milestone)
  - After 3+ meaningful core actions (not just 3 app opens)
  - NOT: on launch, during a task, after an error, or during a paywall flow

Implementation (iOS): SKStoreReviewRequest.requestReview()
  - The system handles the dialog; you can't customize it
  - Apple limits how often the dialog appears per year

Implementation (Android): In-app Review API (Google Play)

Do NOT build a custom modal that asks "Enjoying the app? Rate us 5 stars."
  This violates App Store and Play Store policies.

The pre-prompt strategy (iOS-safe):
  A custom screen that asks "Are you enjoying [App Name]?"
  → "Yes" → trigger SKStoreReviewRequest
  → "Not really" → link to feedback form (not App Store)
  This is a common and accepted pattern.
```

---

## In-app help structure

### Help center organization

```
Organize by user job, not by feature name:

Good structure:
  - Getting started
  - [Primary job 1] (e.g., "Tracking habits")
  - [Primary job 2] (e.g., "Reading your stats")
  - [Primary job 3] (e.g., "Managing reminders")
  - Account and settings
  - Troubleshooting

Avoid:
  - Organizing by feature category (sounds internal, not user-focused)
  - A flat list of all articles with no grouping
```

### Help article template

```
Title: "[Job to be done]" — e.g., "How to export your data"
Not: "Export function" or "Data management"

Body:
  1. One-sentence summary of when to use this
  2. Numbered steps — one action per step
  3. Screenshot or GIF for any non-obvious step
  4. "If this doesn't work:" troubleshooting block

Related articles: 2-3 links at the bottom
"Was this helpful?" feedback prompt at bottom
```

---

## Release notes (App Store changelog)

```
The release notes are onboarding for existing users on every update.

Template for meaningful updates:

  Version [X.X] — [Month Year]

  **What's new:**
  • [Specific new feature] — [one-sentence benefit]
  • [Specific improvement] — [what changed and why it's better]

  **Fixed:**
  • [Specific bug] — e.g., "Fixed a crash when importing from Apple Health"
  • [Specific bug]

For voice guidance, see voice-and-tone.md — "developer/release notes voice" section.

Avoid:
  - "Bug fixes and performance improvements." (Says nothing. Users notice.)
  - Marketing language in release notes. ("Revolutionary new experience!")
  - Internal technical jargon. ("Refactored the auth token handler.")

Goal: A user who reads only the release notes should understand exactly what changed
and whether they'll notice it in their daily use.
```
