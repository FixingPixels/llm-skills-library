# Common Onboarding Failures

Diagnostic guide for onboarding flows that aren't working. Match the symptom to the failure mode and propose targeted fixes. Each failure has a board-game analogue in parentheses — same underlying problem, different surface.

---

## Failure: User arrives in a broken or confusing first state

*(Analogue: Players set up wrong)*

**Symptom**: On first launch, the user sees an error state, a blank screen with no context, or a UI that implies content they haven't created yet.

**Root causes**:
- App defaults to a view that requires existing data (e.g., a feed with no posts, a dashboard with no tracked items, a calendar with no events).
- First-launch state hasn't been designed as a distinct experience — it's the same view as a populated app, minus the content.
- Server or auth errors during account creation aren't handled gracefully.
- Setup steps (profile creation, import, preferences) were skipped or interrupted, leaving the app in a partial state.

**Fixes**:
- Design a distinct first-launch empty state for every major screen. This is a separate design job from the populated state.
- Require zero data to show something useful on first launch. Prefill with a sample, a template, or a clear invitation to create.
- Build graceful error recovery for every first-launch path: failed sign-up, slow network, interrupted setup.
- Add a completion indicator if setup has multiple steps so the user knows where they are.

---

## Failure: User doesn't understand what the app does

*(Analogue: Players don't know the goal)*

**Symptom**: In user tests, participants open the app and within 20-30 seconds say "what is this?" or take a wrong action. In App Store reviews: "I couldn't figure out what to do."

**Root causes**:
- No value proposition screen, or one that uses internal jargon the user doesn't know.
- First screen is a login prompt — the user hasn't seen what they're signing up for.
- App name and subtitle don't state the job clearly.
- The core action is not prominent on the first screen after onboarding.

**Fixes**:
- Add 1-3 value screens before sign-up. Each should state a single benefit, visually. Test by showing each screen for 5 seconds to a stranger — can they say what the app does?
- Never make account creation the first thing a new user sees without showing them the product first.
- Ensure the home screen has one clear primary action visible above the fold.
- State the core job in the app name + subtitle combination (those fields are what users read in the App Store and in Spotlight search).

---

## Failure: Users forget how to do things after coming back

*(Analogue: Players forget rules mid-game)*

**Symptom**: Re-engagement data shows users who return after 7+ days churn quickly. Support tickets are "how do I...?" questions about basic features they used in session 1.

**Root causes**:
- No in-app help or contextual hints on secondary flows.
- Navigation is non-standard or requires memorized gestures.
- The app doesn't communicate its state — users don't know where they are or how to get back.
- The feature exists but isn't discoverable from where the user needs it.

**Fixes**:
- Place a "?" contextual help icon on any screen with non-obvious functionality.
- Use standard navigation patterns (tab bar, back navigation, modal dismissal) that users already know from other apps. Non-standard navigation is a re-engagement tax.
- Send users to the last point of progress on re-launch, not to the home screen — reduce re-orientation cost.
- Build a searchable in-app help section reachable from settings. One search should answer any "how do I" question in under 30 seconds.

---

## Failure: Onboarding copy contradicts the UI

*(Analogue: Rules contradict each other)*

**Symptom**: Onboarding tells the user to tap a button that doesn't exist in that location, or describes a feature using a different name than the one in the UI. Users follow the instructions and arrive somewhere unexpected.

**Root causes**:
- Onboarding copy was written before the final UI was built, then not updated.
- The UI was updated without updating the tooltip, coach mark, or help article that references it.
- Multiple writers used different terminology for the same feature.

**Fixes**:
- Keep a single vocabulary list of feature names. Every piece of copy — onboarding, help center, release notes, App Store listing — must use the same terms.
- Build a review step into every UI change: does anything in onboarding or help reference this element? Update it before shipping.
- If a feature name changes after users are already familiar with it, acknowledge the rename in release notes so returning users can re-orient.

---

## Failure: Users drop off mid-onboarding flow

*(Analogue: Comprehension drops in mid-rulebook)*

**Symptom**: Analytics show a step-function drop at a specific screen in the onboarding sequence. The first two screens have high completion; by screen five, most users have abandoned.

**Root causes**:
- The flow is too long — the user's patience runs out before they see value.
- A specific screen has a high-friction action (fill in a multi-field form, decide something they don't know yet, grant a permission without context).
- The flow front-loads configuration and defers the value demonstration.
- A sign-up form with too many required fields.

**Fixes**:
- Audit every screen: what does the user get from this screen that changes what they see next? If nothing, cut it.
- Move all configuration to post-activation. Get the user to their first value moment with as few screens as possible, then ask for preferences.
- Reduce required sign-up fields to the minimum. Email or social login only for the first screen. Ask for name, photo, preferences later.
- For any high-friction step that can't be removed, add a "set this up later" option.

---

## Failure: Onboarding is too long / users disengage before reaching value

*(Analogue: Players disengage during long teaches)*

**Symptom**: Even users who complete the onboarding flow rate it poorly, or skip it when re-onboarding after reinstalling. Time-to-first-action metrics are high.

**Root causes**:
- The onboarding was designed to explain all features rather than to activate one.
- Too many animations, illustrations, or copy slides before the user can do anything.
- The tutorial is mandatory and can't be skipped.
- The onboarding shows the UI rather than getting the user into the UI.

**Fixes**:
- The goal of onboarding is to reach the first "aha moment" as fast as possible. Every screen that doesn't directly advance toward that moment should be cut or deferred.
- Always include a "Skip" or "I know this" option for every onboarding screen and tutorial. Users who skip still activate — users who are trapped abandon.
- Show, don't tell. Instead of a screen that says "Here's how to create a habit," take the user directly to the creation screen. "Let's create your first habit."
- Benchmark first meaningful action time against competitors. If yours is 3 minutes and a competitor's is 30 seconds, the difference will show in activation rates.

---

## Failure: Help content covers edge cases but not the main flow

*(Analogue: Edge cases dominate the rulebook)*

**Symptom**: The app has a help center, but user support tickets keep coming in for basic questions that "should" be in the help center. Looking at the help center reveals it's full of articles about edge cases, error states, and advanced features — but doesn't explain how to do the core job.

**Root causes**:
- Help content was written reactively — articles were created when users complained, not proactively.
- Core flows seemed obvious to the developer (who knows the app) and were never documented.
- Advanced features got docs because they generated support tickets; basic features didn't get docs because they seemed self-evident.

**Fixes**:
- Write the core 5 help articles first, covering the primary user journeys end-to-end, before writing any edge-case articles.
- Order help articles by user frequency, not by internal feature priority.
- Link contextually from the app to the relevant help article at the moment of likely confusion — not just from a centralized help index.
- Run periodic user research asking "what's the one thing you wish was better documented?" — answers often reveal undocumented core flows.

---

## Failure: Empty state paralysis — user doesn't know what to do first

*(Analogue: New players freeze on first turn)*

**Symptom**: Users complete the sign-up flow and land on the home screen, then do nothing and close the app. Session 1 ends with no meaningful action taken.

**Root causes**:
- The home screen in empty state shows nothing actionable.
- There are multiple possible first actions with no guidance on which to take.
- The create/start action is not visually prominent.
- The app requires input before it can show value (e.g., a budgeting app that shows no data until the user links a bank account, with no guidance on how to do that).

**Fixes**:
- Design the empty home screen around a single, clear CTA. One button. One job. "Track your first expense" is better than a generic "+" and three tabs with empty states.
- Populate the empty state with a realistic example or sample data that shows what the filled state will look like. This reduces uncertainty about whether the user's input is correct.
- For apps that require a setup step before showing value (bank link, calendar import, device pairing), make that step part of onboarding, not a surprise after onboarding.
- Consider a "start with a template" option for creation apps — an empty canvas is more intimidating than a starting point.

---

## Failure: Users confused about what triggered a charge or subscription

*(Analogue: Players dispute scoring)*

**Symptom**: App Store reviews mention unexpected charges. Users email support asking "why was I charged?" Support tickets arrive around renewal dates.

**Root causes**:
- Free trial end date wasn't clearly communicated during sign-up.
- The difference between the free tier and the paid tier isn't visible until the user tries a paid feature.
- IAP purchases don't have clear confirmation screens.
- Renewal pricing and terms weren't shown at subscription sign-up.

**Fixes**:
- On any screen where a subscription starts (including free trials), display: what they're getting, what it costs, when billing starts, and how to cancel.
- Send a push notification or email when a free trial is 1-3 days from ending (if the user has opted into notifications).
- Show the difference between free and paid in the UI continuously — a visible "upgrade to unlock" label is better than a surprise modal when the user taps a locked feature.
- Follow Apple and Google's subscription disclosure requirements precisely. Both app stores review subscription disclosures closely; unclear copy is a common rejection reason.

---

## Failure: Power users work around the onboarding or core flow

*(Analogue: Veterans house-rule the game)*

**Symptom**: Long-term users have found a non-obvious workflow (a sequence of taps, a workaround, a feature combination) that they prefer over the intended flow. Support tickets contain "why doesn't the app just do X?" where X is a workaround users invented.

**Root causes**:
- The intended flow has friction that experienced users have learned to avoid.
- A shortcut or power-user feature exists but isn't surfaced in the main flow.
- User mental models evolved through use and diverged from the design intent.

**Fixes**:
- Treat power-user workarounds as product signal, not a support problem. If enough users are doing X instead of the intended flow, the intended flow has friction worth fixing.
- Surface power-user shortcuts progressively — not in the initial onboarding, but discoverable after the user has established a baseline routine.
- Run interviews with long-term users to understand their actual workflows. The gap between intended and actual behavior is often where the most valuable product improvements hide.

---

## Failure: App Store reviews mention "confusing" or "hard to figure out"

*(Analogue: Online reviews complain about the rulebook specifically)*

**Symptom**: App Store reviews include phrases like "confusing," "couldn't figure out how to," "not intuitive," "had to give up," without specifying which feature.

**Root causes**:
- Usually a combination of the above failures, accumulated.
- Almost always: missing or inadequate empty states, unclear first action, or a permissions cliff that put users off in the first session.
- The developer is too familiar with the app to see what's invisible to newcomers.

**Fixes**:
- Read every 1-star and 2-star review and categorize the complaints. "Confusing" always has a specific cause — find the cluster.
- Run a fresh unmoderated user test with 3-5 people who have never seen the app. Watch where they hesitate, what they misread, what they tap expecting one thing and getting another.
- Identify your 3 reference apps — apps with design you admire in your category — and note what they do in their onboarding that yours doesn't.
- A v2 onboarding update is a legitimate and common App Store update. Frame it in release notes as what you've improved and why.

---

## Mobile-specific failure: Notification permission asked too early

**Symptom**: Push notification opt-in rate is very low (under 30-40%). Users who denied notifications have significantly lower 30-day retention than those who accepted.

**Root causes**:
- The notification permission prompt appears on first launch, before the user has any reason to want notifications.
- No custom pre-prompt explains what kind of notifications the user will receive and why they're valuable.
- The app depends on notifications for its core loop (e.g., habit reminders, event alerts) but the user never saw that loop before being asked.

**Fixes**:
- Move the notification permission ask to after the user's first successful core action, or after they've seen the feature that requires notifications.
- Always precede the system permission dialog with a custom screen: "To remind you to log your mood each evening, we'll send a gentle nudge. You choose the time." The system prompt then follows — framed by context.
- If the user declines, offer an in-app alternative (e.g., a reminder they have to set manually) and periodically surface a soft re-ask in context ("Want a reminder? Enable notifications in settings.").

---

## Mobile-specific failure: Permissions cliff

**Symptom**: Large drop-off during onboarding at a specific step. On exit-survey data, users mention "it asked for too many permissions" or "I didn't understand why it needed that."

**Root causes**:
- Multiple permission requests are presented in sequence during setup before the user has seen value.
- Permission request copy is vague or uses the platform default string ("Allow X to access your Location?") without a custom rationale.
- The app is requesting permissions it doesn't need yet, or ever.

**Fixes**:
- Audit every permission the app requests. If it's not needed for the primary use case in the first session, defer the ask.
- Write a custom purpose string for every permission. Be specific: "To show you nearby coffee shops" is better than "To access your location."
- Space permission asks — never ask for more than one permission per session until the user has established a pattern with the app.
- Request only the minimum access level. "When in use" location before "Always on." Read-only contacts access before write access.

---

## Mobile-specific failure: Paywall too early

**Symptom**: Subscription or IAP conversion rate is low. Users who see the paywall in session 1 convert at much lower rates than users who see it in session 3+.

**Root causes**:
- The paywall appears before the user has experienced the feature they're being asked to pay for.
- The free tier has so little functionality that the user hasn't been able to evaluate the product.
- The paywall is triggered by a feature the user stumbled into accidentally, not one they sought out intentionally.

**Fixes**:
- Ensure the user has experienced the core value of the app (and ideally, has performed the core action at least once) before encountering the paywall.
- Design the paywall around a specific moment of desire: the user has tried to do X, liked it, and now wants more of it. That is the right time to offer more.
- Show the paywall with context: "You've logged 3 habits this week. Unlock unlimited habits and detailed analytics for $X/month." Specific, earned, relevant.
- For subscription apps, the free trial should cover enough of the core experience that the user has formed a habit or seen clear value before billing starts.
