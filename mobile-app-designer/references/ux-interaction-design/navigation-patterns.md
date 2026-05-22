# Navigation Patterns

Quick reference of common mobile navigation structures and what they're good for. Use to help a builder choose a navigation architecture deliberately rather than defaulting to "I'll figure it out as I go."

## Tab bar (bottom navigation)

Persistent tabs at the bottom of the screen. Each tab is a top-level destination; tapping a tab always returns to the root of that section.

- **Good for**: Apps with 2–5 distinct top-level areas of roughly equal importance that users switch between frequently. Social apps, content consumption, productivity hubs. (Instagram, Twitter/X, Spotify, Notion mobile.)
- **Bad for**: Apps with a single primary flow, apps with more than 5 top-level sections, apps where hierarchy is more important than lateral movement.
- **Platform note**: Native to iOS. Android supports it via Material bottom navigation but a nav drawer has been more conventional historically — though this is shifting.
- **Tightening**: Label every tab with a word, not just an icon (until the app is extremely well-known). Tab count sweet spot is 3–4. Hide the tab bar inside immersive content views (video, maps, camera) but restore it reliably.

## Stack navigation (push/pop)

A linear hierarchy where each screen pushes onto a stack; the user drills in and swipes or taps back to go up.

- **Good for**: Content with clear hierarchy — browse → list → detail. Checkout flows, settings, article readers, onboarding sequences. Almost every app uses stack navigation for *something*.
- **Bad for**: Anything requiring frequent lateral movement between peers at the same level. Deep stacks (4+ levels) produce orientation loss — users forget how they got there.
- **Platform note**: Foundational to iOS UINavigationController. Android's back stack works similarly but the back gesture/button is system-level. Swipe-back is a strong iOS convention; don't disable it without strong reason.
- **Tightening**: Keep stacks shallow. If users commonly go 3+ levels deep, consider whether the middle level is doing real work or is just a list that could be replaced by search. Use descriptive back button labels on iOS (the title of the previous screen, not just "Back").

## Modal / bottom sheet

A view that slides up over the current context, used for focused tasks, confirmations, or supplementary detail without fully navigating away.

- **Good for**: Completing a short sub-task without losing context (compose a reply, add a tag, confirm a destructive action, show a detail card). Works well when the user needs to return to exactly where they were.
- **Bad for**: Complex multi-step flows. If the task inside a modal requires more than 2–3 interactions, it probably deserves its own screen. Avoid modals that present other modals.
- **Platform note**: iOS bottom sheets and full-screen modals are native patterns with well-defined dismiss behaviour (swipe down). On Android, Material bottom sheets have similar conventions.
- **Tightening**: Give every modal a clear dismiss affordance. Don't use modals for errors — use inline feedback instead. If users are confused about whether they're in a modal or a new screen, the visual treatment needs work.

## Full-screen modal flow

A sequence of modal screens that takes the user through a contained task before returning them to their origin — onboarding, subscription flow, camera/capture, permissions sequence.

- **Good for**: Focused sequences with a clear start and end where the normal navigation chrome would be distracting (onboarding, checkout, camera, setup wizard).
- **Bad for**: General navigation. This pattern says "you're in a special mode now" — if it's used too often, users feel trapped.
- **Tightening**: Always give users an escape (a dismiss or skip at the start). Show progress when the sequence is more than 3 steps. Return to exactly the right place in the app when the flow ends — don't drop users at the home screen.

## Drawer / side navigation

A panel that slides in from the side, usually containing top-level destinations or account/profile access.

- **Good for**: Apps with many top-level sections where a tab bar would be overcrowded. Content-heavy apps where navigation is less frequent than consumption (Gmail, Slack — though Slack has since moved to a bottom tab).
- **Bad for**: Apps where navigation is frequent (the swipe-to-open gesture competes with list-swipe actions). Apps where discoverability of sections matters — the drawer hides navigation behind a gesture or a hamburger icon.
- **Platform note**: More native on Android; feels slightly off on iOS where users expect bottom-tab or stack patterns. A hamburger menu on iOS often signals that the app was designed for Android first, or that the IA hasn't been resolved.
- **Tightening**: If the drawer primarily contains settings and account items, consider whether those belong in a Profile tab instead. Reserve the drawer for apps with genuinely many top-level destinations that are visited infrequently.

## Gesture-first navigation

Core navigation driven by swipes, long presses, or other gestures rather than tap targets — used to add speed for power users or to build spatially coherent experiences.

- **Good for**: Apps where speed matters to experienced users and the gesture is learnable over time (email clients, to-do apps, map-adjacent apps). Can dramatically reduce tap count.
- **Bad for**: New-user flows. Gestures are invisible; if a user doesn't know the gesture exists, the feature doesn't exist for them. High-risk for discoverability failures.
- **Tightening**: Always provide a non-gesture alternative for every gesture action. Introduce gesture shortcuts *after* the user has learned the basics — not on first launch. Animate gestures in onboarding or via empty-state hints rather than expecting discovery.

## Search-as-navigation

The primary way to find content is search rather than browsing a hierarchy.

- **Good for**: Apps with large, flat content libraries where hierarchy would require arbitrary categorisation (notes, files, contacts, messages). Acts as a shortcut that bypasses deep navigation stacks.
- **Bad for**: Apps where browsing and discovery are core to the experience — forcing users to search what they don't yet know to look for breaks the experience.
- **Tightening**: Make search prominent and persistent — not buried in a tab or a small icon. Show recent searches and smart suggestions before the user types. Pair with browse for new users who don't have enough context to search effectively.

## Choosing a structure

Don't pick a pattern first and design into it. Pick a pattern because:

1. It matches how frequently users move between sections (tabs for frequent lateral movement; stack for infrequent, hierarchical movement).
2. It fits the platform's native conventions for your primary audience.
3. It handles your most frequent user action in the fewest taps.
4. It stays coherent when the app grows — don't paint yourself into a corner with a structure that can't accommodate a second core feature.

If two patterns fit, prototype both. A 30-minute sketch test with two people will tell you more than an hour of discussion.
