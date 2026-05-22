# Common UX Failure Modes

Diagnostic guide for the most frequent ways mobile app interaction systems break. When a builder reports something feels off, walk through these to find the match.

## Option overload

**Symptom**: Users stall on a screen, make the wrong choice, or leave without acting. Screens feel busy even when they're not long.

**Diagnoses**:
- Too many choices presented at the same level of hierarchy.
- Decisions are too consequential relative to the information given (users are afraid to be wrong).
- Labels aren't distinct enough — users can't tell what the difference between two options is.

**Fixes to try**:
- Default to one primary action per screen; secondary actions can be accessible but visually subordinate.
- Add progressive disclosure — show the most important options first, let users expand for more.
- Improve labels: replace generic verbs ("Continue", "OK") with specific ones ("Save note", "Delete forever").
- Reduce choice by making the best option the default — users opt out rather than opt in.

---

## Rage tap

**Symptom**: Users tap the same element repeatedly, sometimes in frustration. Analytics shows multiple rapid taps on the same target.

**Diagnoses**:
- No visual feedback that the tap registered (button didn't change state).
- Response latency is long enough that users assume the first tap didn't work.
- The tap target is too small and users aren't confident they hit it.

**Fixes to try**:
- Add immediate visual feedback on every tap — a press state, a spinner, a brief colour change. Happens before any network call.
- Disable the button after first tap and show a loading state.
- Audit tap target sizes: minimum 44×44pt on iOS, 48×48dp on Android.
- If latency is unavoidable, add an optimistic UI — assume success, update the screen immediately, reconcile in the background.

---

## Confusion loop

**Symptom**: Users navigate back and forth between the same two or three screens. Session recordings show repetitive patterns. Users ask "how do I…?" about features that exist.

**Diagnoses**:
- The navigation structure doesn't match users' mental model of the app.
- A feature is in a place users wouldn't think to look.
- Labels or icons aren't communicating what a section actually contains.

**Fixes to try**:
- Card-sort test: show users a list of the app's features and ask them to group them as they'd expect to find them. Compare to the actual structure.
- Rename sections or features to match how users describe them, not how the builder thinks about them.
- Add cross-links or shortcuts from likely wrong locations to the right one.
- Consider whether the navigation structure needs a deeper fix — symptoms often survive surface relabelling.

---

## Engagement cliff

**Symptom**: Strong day-1 retention, significant drop-off by day 3 or day 7. Users open the app a few times then stop.

**Diagnoses**:
- The app delivered its promise once, but there's no clear reason to return.
- The core value is consumed on first use and users don't know there's more.
- Notifications were either never enabled or are being sent but aren't relevant enough to re-engage.

**Fixes to try**:
- Identify the "aha moment" and ask: what happens after it? Is there a second aha moment?
- Build a re-engagement hook into the core loop — something new or personal to come back to.
- Review notification strategy: frequency, timing, content relevance. One well-timed relevant notification outperforms ten generic ones.
- Add an empty state or prompt that surfaces on return visits and points to the next valuable action.

---

## Onboarding abandonment

**Symptom**: Users drop off during onboarding — either immediately, or partway through a setup sequence.

**Diagnoses**:
- Onboarding asks for too much before delivering any value.
- A permissions request (contacts, location, notifications) appears before users have reason to grant it.
- The sequence is too long — users feel like they're filling out a form, not discovering a product.
- The value proposition in the onboarding copy doesn't match what users actually get.

**Fixes to try**:
- Delay every permission request until the moment the user tries to use the feature that needs it.
- Cut onboarding to the minimum needed to reach the first moment of value. Everything else can wait.
- Show something useful before asking for anything. Let users experience value before asking for their email.
- Test the first 60 seconds specifically — that's where most abandonment happens.

---

## Permission cliff

**Symptom**: A feature that requires device permissions (notifications, location, camera, contacts) is never used by most users, or users complain it "doesn't work."

**Diagnoses**:
- The permission was requested too early — before the user understood why the app needs it.
- The system permission dialog appeared with no context, and the user denied it reflexively.
- After denial, the app doesn't explain how to re-enable the permission or gracefully degrade without it.

**Fixes to try**:
- Show a pre-permission screen that explains what the permission enables and why it makes the app better. Frame it as a benefit, not a requirement.
- Request permissions at the moment of use, not at launch.
- After a denial, offer a path to re-enable in Settings. Don't silently break the feature.
- Design a graceful degraded experience for users who don't grant the permission — the feature should still exist in a limited form if possible.

---

## Paywall friction

**Symptom**: Low conversion from free to paid. Users reach the paywall and leave rather than subscribe or purchase.

**Diagnoses**:
- The paywall appears before users have experienced enough value to justify paying.
- The value proposition on the paywall screen doesn't match what users actually care about.
- The price feels high relative to the value users have experienced.
- The paywall is too aggressive — users feel trapped rather than persuaded.

**Fixes to try**:
- Audit where the paywall appears relative to the user's first experience of value. Push it later.
- Test the paywall copy: be specific about what paid unlocks ("Unlimited notes + offline access" beats "Go Pro").
- Offer a free trial rather than an immediate payment ask — especially for subscriptions.
- Ensure users can dismiss the paywall and continue in free mode. A hard gate before value is experienced kills conversion.

---

## Silent churn

**Symptom**: Retention metrics show users stopping without any visible signal. No uninstalls tracked, no complaints — they just stop opening the app.

**Diagnoses**:
- The app has low notification permissions, so there's no re-engagement channel.
- The core loop delivered value once but didn't create a habit.
- A friction point built up over time — a bug, a slow screen, a flow that got slightly worse — and users quietly gave up.

**Fixes to try**:
- Instrument session frequency and identify which cohorts churn — when do they drop off and what was their last action?
- Send a lightweight win-back prompt at the point where churn typically starts (day 5, day 14 — whatever your data shows).
- Look at the last screen users visited before their final session — is there a pattern? That screen may be a silent exit point.
- Check for gradual degradation: a screen that worked fine at launch but now has more content and is slower to load.

---

## The expert trap

**Symptom**: The builder thinks the app is easy to use; new users consistently struggle. What seems obvious to the builder is invisible to users.

**Diagnoses**:
- The builder has used the app for months and no longer sees what a new user sees.
- Features that require learning have no onboarding, because the builder forgot they needed to learn them too.
- Navigation relies on icons or gestures that are intuitive once known but opaque on first encounter.

**Fixes to try**:
- Watch three people use the app who have never seen it before. Don't explain anything. Take notes.
- Audit every gesture and non-standard icon: if a user wouldn't understand it without trying it, add a label or a hint.
- Keep a "stupid questions" list from every early user — what did they ask about that seemed obvious? Those are design failures, not user failures.

---

## Diagnostic prompts to ask the builder

When they report a problem, before proposing a fix:

- "At what point in the flow did it go wrong — which screen, which action?"
- "What did users do when they got stuck — leave, try something random, contact you?"
- "Did one specific type of user struggle, or was it everyone?"
- "What did you think they would do at that point?"
- "If you watched them on a screen recording, what would you have seen?"
