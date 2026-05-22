---
name: technical-architecture
description: >-
  This skill should be used when the user needs to make platform or stack decisions before
  writing code. Trigger on: "should I build native or cross-platform", "React Native vs Flutter",
  "iOS or Android first", "what backend should I use", "Firebase vs Supabase", "do I need a
  server", "what stack should I use", "how do I handle auth", "push notifications setup",
  "what do I build first", or any question about platform choice, framework selection, or
  backend architecture for a mobile app.
---

# Technical Architecture

Help the builder make the **platform and stack decisions** that precede writing code — before they've committed to a framework that's hard to reverse.

These decisions have long tails: the wrong platform choice affects hiring, App Store approval friction, performance ceiling, and maintenance cost for years. The goal isn't to prescribe a stack. It's to surface the constraints — team size, technical background, target market, timeline, performance requirements — that make one option clearly better than the alternatives for *this* builder.

## Operating mode: Socratic, constraint-first

Don't recommend a stack on the first message. Most builders frame their question as a technology choice when the real question is about their constraints. Ask those first.

The sequence:

1. **Who is building this?** Solo founder with a full-time job, solo technical founder, two-person team? Technical background — has this person shipped a mobile app before? What do they already know?
2. **What does the app do, specifically?** "Social app" is too vague. Push for: what is the primary interaction? Does it need real-time sync? Heavy native device access (camera, Bluetooth, GPS, health data)? Offline-first? The answers eliminate options fast.
3. **Who is the target user, and on what platform?** Consumer app with a broad audience → iOS-first usually wins on revenue, Android-first on reach. B2B or enterprise tool → follow what the buyer's company issues. Niche or hardware-adjacent → often only one platform matters.
4. **What is the timeline and budget?** "I want to launch in three months" narrows choices. Cross-platform frameworks reduce upfront cost; native gives more control later. Identify which constraint is binding.
5. **What does "good enough" look like for v1?** Some builders need pixel-perfect platform-native feel from day one. Others need to validate the idea with any working app. The right answer is different.

Only after these answers are clear — propose options with tradeoffs. Don't propose all options every time. Propose the one or two that fit the constraints, and explain why the others don't.

## The platform decision

### iOS-first

**Fits when**: consumer app, English-speaking or Western European market, monetising via subscriptions or premium purchase, builder has a Mac, team is small (iOS codebase is smaller to maintain solo).

**What people miss**: The App Store review process is slower and more likely to reject edge-case features. Apple's human interface guidelines are enforced — breaking them costs approval time. TestFlight is excellent for beta distribution. iOS users spend more per user than Android on average, which matters if revenue-per-user is the model.

### Android-first

**Fits when**: emerging markets (Southeast Asia, India, Latin America, Sub-Saharan Africa), hardware integrations (some peripherals have Android SDK only), enterprise or B2B tools where IT issues Android devices, games with ad monetisation (Android volume is higher), or builder already knows Kotlin/Java.

**What people miss**: Google Play review is faster and more permissive, but also more variable — malware filters can flag legitimate apps. Fragmentation across device manufacturers is real for anything that touches camera, Bluetooth, or sensors. Android users are more price-sensitive on average; subscription conversion is lower than iOS.

### Cross-platform (React Native, Flutter, Expo)

**Fits when**: solo or small team with limited native experience, identical functionality on both platforms, timeline is binding, the app's primary interface is lists/forms/content (not heavy animation, gaming, or deep native APIs), backend iteration speed matters more than pixel-perfect native behaviour.

**What people miss**: Cross-platform is not "one codebase, no compromise." Platform divergences leak through constantly — push notification handling, keyboard behaviour, gesture conflicts, native module bridging, App Store and Play Store compliance differences. Budget extra time for platform-specific bugs.

See [platform-decision-guide.md](../../references/technical-architecture/platform-decision-guide.md) for the full comparison matrix and downstream effects.

## The framework question (cross-platform)

**React Native / Expo**: JavaScript/TypeScript. Huge ecosystem. Expo dramatically lowers setup friction and handles many native pain points (OTA updates, build service, push notifications). Good choice if the builder already knows JS/TS or is coming from a web background. Expo Go is excellent for rapid prototyping.

**Flutter**: Dart. Smaller ecosystem but growing fast. Renders its own widget layer rather than mapping to native components — this means pixel-identical across platforms, but the widgets look slightly non-native by default (fixable, but requires effort). Performance ceiling is higher than React Native for animation-heavy apps. Better choice if the builder is willing to learn Dart and wants fine-grained control over rendering.

**What to avoid recommending**: Ionic, Capacitor, or web-wrapped apps for anything that requires a native-feeling experience. These are fine for internal tools or B2B dashboards; they feel wrong for consumer apps.

## The backend decision

### No backend (local-first)

**Fits when**: the app works entirely from data on the device — offline calculators, habit trackers, journaling apps, single-player games, personal finance tools where cloud sync is optional. Simplest possible architecture. v1 of many successful indie apps started here.

**What to add later**: iCloud (via CloudKit or NSUbiquitousKeyValueStore) for iOS-only sync without a server. This gets you cross-device sync on Apple hardware with no backend to maintain.

### Firebase

**Fits when**: real-time data sync is core (chat, collaborative features, live feeds), the builder wants a managed service with no server config, push notifications via FCM, Google Analytics integration. Firestore is the default choice for document-oriented data.

**What people miss**: Firebase pricing has surprised many indie apps — the free tier is generous, but Firestore reads at scale (especially with poorly-structured queries or aggressive listeners) can cause unexpected bills. Security rules are unintuitive and critical to get right before shipping. Firebase Lock-in is real: migrating off it later is painful.

**Auth**: Firebase Auth handles email/password, Google, Apple (required for iOS if you offer any third-party auth), and phone auth well. Apple Sign-In is mandatory on iOS if you offer any social login — review rejection otherwise.

### Supabase

**Fits when**: the builder is comfortable with SQL and relational data models, wants Postgres under the hood, wants row-level security that's easier to reason about than Firestore rules, or has prior experience with relational databases. Open-source — can self-host later.

**What people miss**: Supabase's realtime features are less mature than Firebase's. The SDK for mobile is solid but Firebase has more tutorials, Stack Overflow answers, and ecosystem tooling. Good choice for builders with a backend or SQL background; steeper learning curve than Firebase for first-timers.

### Custom backend

**Fits when**: the builder has specific requirements that managed services don't support (custom authentication flows, existing company infrastructure, specific compliance requirements), or they have prior backend experience and know what they're doing.

**What to defer**: For almost all indie apps at v1, a custom backend is premature. Firebase or Supabase will get you to launch; switch if and when you hit a wall.

See [stack-tradeoffs.md](../../references/technical-architecture/stack-tradeoffs.md) for the full backend comparison and common indie-scale architecture patterns.

## Things that trip indie developers up

**Auth with Apple Sign-In**: If your iOS app offers any third-party sign-in (Google, Facebook, Twitter), Apple requires you to also offer Sign-In with Apple. Missing this causes App Store rejection. Firebase Auth and Supabase both support it — but it requires an Apple Developer account, correct entitlements, and a backend endpoint to exchange tokens. Don't discover this on submission day.

**Push notifications are more work than they look**: The happy path (send a push, it appears on screen) is easy. The edge cases — permission denied, background fetch, notification actions, deep linking from a notification, handling notifications when the app is in the foreground vs. background vs. killed — add up to a week of integration work. Plan for it.

**App size and startup time**: Every dependency adds to app size and startup time. Indie apps that try to include every SDK (analytics, crash reporting, A/B testing, ads, attribution) during development often ship bloated. Add what you need; defer what you might need.

**Over-engineering before validation**: The most common technical mistake at indie scale is building a sophisticated, scalable backend before validating that anyone wants the app. The goal of v1 is to learn, not to scale. Firebase with a simple Firestore schema is almost always the right call for the first version of a consumer app.

## What to avoid

- **Recommending a stack without understanding the builder's constraints first.** The right stack for a solo founder with no mobile experience is different from the right stack for a web engineer who knows TypeScript.
- **Getting drawn into "which is better" debates** (React Native vs. Flutter, Firebase vs. Supabase) without grounding the answer in the builder's specific situation.
- **Scope creep into implementation.** Architecture decisions are in scope. Writing the actual code or debugging specific SDK integrations is not — point toward documentation and community resources.
- **Ignoring the App Store rules** as a technical constraint. Apple and Google's requirements (Apple Sign-In, privacy manifests, 64-bit compliance, etc.) are not optional. Flag them early.

## Reference files

- [platform-decision-guide.md](../../references/technical-architecture/platform-decision-guide.md) — iOS vs Android vs cross-platform comparison matrix, downstream effects on hiring, approval, and maintenance
- [stack-tradeoffs.md](../../references/technical-architecture/stack-tradeoffs.md) — backend options, auth, push notifications, and common indie-scale architecture patterns

## Handoffs

- Platform decided, now designing interaction flows → [ux-interaction-design](../ux-interaction-design/ux-interaction-design.md)
- Stack decided, now thinking about monetisation model and infrastructure it implies → [monetization-strategy](../monetization-strategy/monetization-strategy.md)
- Architecture driven by an unclear product scope → back to [product-ideation](../product-ideation/product-ideation.md)
- Visual identity and UI system → [ui-visual-design](../ui-visual-design/ui-visual-design.md)
