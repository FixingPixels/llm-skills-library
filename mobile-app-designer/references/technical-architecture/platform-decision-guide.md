# Platform Decision Guide

Choosing between iOS-first, Android-first, and cross-platform is one of the few early decisions that's genuinely hard to reverse. Use this guide to help a builder pick deliberately rather than defaulting to what they've heard.

---

## The core question before anything else

**Who is your user, and what do they already have in their pocket?**

Every other consideration is secondary. If you know the answer to this, the platform choice usually follows directly.

---

## iOS-first

### When it fits

- Consumer apps targeting North America, Western Europe, Australia, Japan
- Apps monetised via subscription or premium purchase — iOS users convert and spend at higher rates than Android across almost every category
- Solo builder with a Mac and limited capacity to maintain two separate codebores
- Apps that need to feel "premium" — the association with higher-income demographics is real and affects positioning
- Health and fitness apps (Apple Health / HealthKit integration is deeper and more trusted than Android Health Connect)
- Apps with sensitive data (iOS has a stronger privacy reputation with users)

### Revenue reality

On average, App Store revenue per download is 2–4× Google Play. For subscription apps in particular, iOS users churn at lower rates. If you're building a business around subscriptions, iOS is where the economics work better.

### What to budget for

- App Store review takes 1–3 days for new submissions, sometimes longer for first submissions or significant changes. Plan launch windows accordingly.
- Apple's human interface guidelines are enforced. Apps with non-standard UI patterns get rejected. Budget time to bring the app into compliance before each major submission.
- App Store Connect can be frustrating — rejections are sometimes arbitrary, the appeals process is slow, and policy changes happen without much notice.
- SwiftUI is the modern iOS framework and is good, but still has rough edges for complex apps. UIKit is stable and more battle-tested.

### Downstream effects

| Factor | iOS |
|--------|-----|
| Hiring | Easier to find skilled SwiftUI/UIKit engineers than Kotlin engineers in many markets |
| Review friction | Higher — Apple enforces HIG, privacy manifests, and policy aggressively |
| Monetisation ceiling | Higher per-user revenue in subscription model |
| Device fragmentation | Low — Apple controls hardware; limited screen sizes to design for |
| Long-term maintenance | One language (Swift), one SDK, one store |

---

## Android-first

### When it fits

- Apps targeting Southeast Asia, India, Latin America, Sub-Saharan Africa, Eastern Europe — Android market share dominates in these regions (often 80–90%)
- Enterprise or B2B tools where the company issues Android devices (common in logistics, field service, healthcare in some markets)
- Hardware-paired apps — some Bluetooth peripherals, industrial devices, and IoT hardware ship Android-only SDKs
- Games or content apps where volume matters more than revenue-per-user
- Apps that need sideloading or distribution outside the store (Android allows this; iOS does not)
- Builder already knows Kotlin or Java

### What to budget for

- Device fragmentation is real. Camera, Bluetooth, GPS, and sensor behaviour varies meaningfully across manufacturers (Samsung, Xiaomi, OnePlus, Oppo). Anything that touches hardware needs to be tested on physical devices from major manufacturers, not just emulators.
- Google Play review is faster (often hours, not days) but can flag legitimate apps — the automated malware detection is aggressive and sometimes wrong. Expect to appeal at least once.
- Android users are more price-sensitive on average. Subscription conversion is lower. Ad monetisation often makes more economic sense for high-volume, Android-first apps.

### Downstream effects

| Factor | Android |
|--------|---------|
| Hiring | Kotlin engineers more common in some markets; Java ecosystem very large |
| Review friction | Lower — Play review is faster and more permissive |
| Monetisation ceiling | Lower per-user subscription revenue; better for ad-supported models |
| Device fragmentation | High — dozens of manufacturers, varying hardware and Android versions |
| Long-term maintenance | More complex — more test devices needed, more edge cases |

---

## Cross-platform (React Native / Expo / Flutter)

### When it fits

- Solo or two-person team with no existing native mobile experience
- The app's primary UI is lists, forms, cards, and content — not heavy animation, 3D, or deep device hardware access
- Timeline is the binding constraint — one codebase ships faster than two
- The builder knows JavaScript/TypeScript (React Native/Expo) or is willing to learn Dart (Flutter)
- The product hypothesis hasn't been validated yet — cross-platform reduces the cost of being wrong

### The honest tradeoff

Cross-platform does not mean "no platform differences." It means "platform differences are handled at the framework level rather than the language level." The differences still exist:

- Push notification handling differs between iOS and Android
- Keyboard avoidance behaviour differs
- Back gesture handling differs (Android hardware/system back vs. iOS swipe-back)
- Native module bridging (when you need device APIs the framework doesn't expose) requires writing native code anyway
- App Store compliance requirements (privacy manifests, 64-bit compliance) still apply to both platforms independently

Budget an extra 20–30% of time for cross-platform, platform-specific bugs compared to going native on a single platform.

### React Native / Expo

- **Good for**: Builders with JS/TS background, apps that lean on the npm ecosystem, teams that want Expo's managed workflow (builds in the cloud, OTA updates, pre-wired push notifications).
- **Expo Go** is excellent for rapid prototyping — share a QR code and collaborators can see the running app on their phone without installing anything.
- **Expo EAS** (build service) handles signing and submission — saves significant time.
- **React Native's new architecture** (Fabric/JSI) has matured to the point that the performance complaints from earlier versions are largely resolved — confirm current status against the React Native release notes before quoting specifics to the builder.

### Flutter

- **Good for**: Builders who want consistent pixel-level rendering across platforms, builders building animation-heavy or design-forward apps, teams willing to learn Dart.
- Flutter renders its own widget layer — widgets look identical on iOS and Android by default. This is a feature (consistency) and a drawback (they don't feel fully native unless you deliberately style them to match platform conventions).
- Flutter's performance ceiling for complex animations is higher than React Native.
- Dart has a smaller ecosystem than JavaScript — fewer packages, but the quality of core Flutter packages is generally high.

### What to avoid

- **Ionic / Capacitor / Cordova** for consumer apps. These wrap a web app in a native shell. The performance and feel are noticeably worse than native or RN/Flutter. Fine for internal tools; wrong for consumer-facing apps where first impressions matter.
- **Mixing frameworks mid-project.** If you start with Expo, stay with Expo. If you start with Flutter, stay with Flutter. Framework migrations are expensive.

### Downstream effects

| Factor | Cross-platform |
|--------|---------------|
| Hiring | Larger talent pool (JS developers for RN; Flutter growing fast) |
| Review friction | Same as native for the respective stores |
| Monetisation ceiling | No inherent difference — determined by platform, not framework |
| Device fragmentation | Partially handled by framework, but hardware quirks still leak through |
| Long-term maintenance | Lower initial cost; higher cost when you hit framework limits |

---

## Decision checklist

Use this to work through the choice with a builder:

1. **Who is the primary user?** Where do they live? What device do they carry?
2. **Does the app need deep device hardware access?** (Camera ML, Bluetooth LE, HealthKit, ARKit, specific peripherals) → Each API has platform support implications.
3. **What is the primary monetisation model?** Subscription → favour iOS. High volume + ads → Android may win. Both → cross-platform becomes more attractive.
4. **What does the builder already know?** Swift/SwiftUI → iOS native. Kotlin → Android native. JS/TS → React Native/Expo. Willingness to learn → Flutter is viable.
5. **What is the timeline?** 3 months → cross-platform reduces risk. 12 months → native on primary platform may be worth the investment.
6. **Is the idea validated?** Pre-validation → cross-platform reduces waste. Post-validation, growing → native gives more control at scale.

No tool answers these for you. The answer to each question narrows the option set.
