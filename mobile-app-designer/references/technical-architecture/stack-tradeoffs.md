# Stack Tradeoffs

Reference for backend, auth, push notification, and infrastructure decisions at indie scale. Most indie apps are over-engineered at v1 and under-engineered by v2. This guide helps locate the right level.

> **Verify current pricing and tier limits before committing.** Vendor prices, free-tier ceilings, and Apple/Google platform requirements shift regularly. Use the figures here for shape and order-of-magnitude reasoning — check each vendor's pricing page before the builder picks a stack.

---

## The default indie stack (what most solo builders should use)

Before exploring options, name the default:

**Expo (React Native) + Supabase or Firebase + Expo Notifications**

This combination:
- Works on both iOS and Android from one codebase
- Handles auth, database, file storage, and push notifications without a custom server
- Has extensive documentation and community support
- Gets a solo developer to launch without DevOps knowledge
- Costs $0–$25/month until meaningful scale

If a builder has a specific reason to deviate from this, explore why. Often the reason is "I heard Flutter is better" rather than a genuine constraint.

---

## Backend options

### No backend / local-first

**How it works**: All data lives on the device. No network calls, no accounts, no server.

**Fits**: Single-player or personal tools — habit trackers, journaling apps, offline-capable calculators, flashcard apps, budgeting tools, single-player games.

**Sync options without a custom server**:
- **iCloud / CloudKit** (iOS only): Apple's built-in sync. Free, works across user's Apple devices, respects iOS privacy model. Limited querying capability — document-oriented or key-value. Appropriate for personal data the user owns.
- **iCloud Key-Value Store**: For small preference data (< 1 MB). Very simple API.

**When to grow out of it**: When users want to access their data on multiple devices or share it with others.

---

### Firebase (Google)

**Products**: Firestore (document database), Firebase Auth, Firebase Storage, Firebase Cloud Messaging (push), Firebase Analytics, Crashlytics.

**Fits**: Real-time sync (chat, collaborative editing, live feeds), consumer apps with social features, builders who want a fully managed platform with no server configuration, apps where the "no offline, no backend" question hasn't been answered yet.

**Firestore data model**: Documents inside collections. Flexible schema — you can store any JSON-like structure. Queries are limited compared to SQL (no joins, limited OR queries, no full-text search). Good for user-owned data; awkward for relational data with many cross-references.

**Pricing gotchas**:
- Free tier (Spark plan): 50K reads/day, 20K writes/day, 1 GB storage. Generous for early apps.
- Paid tier (Blaze/pay-as-you-go): Firestore reads cost $0.06/100K. At scale with aggressive listeners or poorly structured queries (e.g., loading full collections on every app open), costs can spike unexpectedly.
- Always add budget alerts in the Firebase console before going live.

**Security rules**: Firestore uses a custom rules language to control read/write access. These are critical — misconfigured rules expose all user data. The learning curve is real. Allocate time to write and test rules before shipping.

**Apple Sign-In with Firebase**: Apple requires Sign-In with Apple on iOS apps that offer any third-party login. Firebase Auth supports this but it requires: an Apple Developer account, an App ID with Sign In with Apple capability, a Services ID for the web redirect flow, and a key from Apple. This takes 2–4 hours to configure the first time. Do not leave it until submission.

---

### Supabase

**Products**: Postgres database (hosted), Auth, Storage, Realtime (via Postgres logical replication), Edge Functions.

**Fits**: Builders with SQL background, apps with relational data (multiple entity types with foreign keys), teams that want row-level security expressed in SQL rather than Firestore rules, apps where avoiding vendor lock-in matters.

**Data model**: Standard relational Postgres. Full SQL — joins, views, functions, full-text search. Row-level security (RLS) uses SQL policies — expressive and auditable, but requires understanding SQL security models.

**Pricing**:
- Free tier: 500 MB database, 1 GB storage, 2 GB bandwidth. Paused after 1 week of inactivity on free tier — use a cron job or upgrade to keep it alive.
- Pro plan: $25/month for small production apps. Predictable.

**Realtime**: Supabase Realtime broadcasts changes via WebSocket subscriptions. Less mature than Firestore's realtime listeners — adequate for most apps, but fewer edge cases are handled out of the box.

**Mobile SDK**: The `supabase-js` client works in React Native via Expo. The Flutter SDK is also well-maintained. More manual setup than Firebase in some areas (push notifications, for example, require a separate provider).

---

### Custom backend

**When it makes sense**:
- The builder has prior backend experience and specific requirements (custom auth flows, existing company APIs, specific compliance or data residency requirements).
- The app needs functionality that managed services don't support well (complex server-side processing, custom webhooks, long-running jobs).
- Team has grown past indie scale and now has dedicated backend engineers.

**Common choices at indie scale**:
- **Node.js / Express or Fastify** — Fast to build, large ecosystem, shares language with React Native.
- **Python / FastAPI** — Good for ML-adjacent features, easy to prototype.
- **Railway, Render, or Fly.io** for hosting — dramatically lower ops burden than AWS/GCP at indie scale.

**What to defer**: At v1, custom backends are almost always premature. Firebase or Supabase gets you to launch. Switch if and when you hit a specific wall — not before.

---

## Auth

### The Apple Sign-In requirement

If your iOS app offers sign-in via any third-party identity provider (Google, Facebook, Twitter, GitHub), Apple requires you to also offer Sign-In with Apple. This is enforced at App Store review — missing it causes rejection.

Both Firebase Auth and Supabase Auth support Apple Sign-In. The configuration requires:
1. An active Apple Developer account ($99/year)
2. An App ID with the Sign In with Apple capability enabled in Identifiers
3. A Services ID (for the redirect URI — even for mobile apps, the web flow is used)
4. A private key from Apple (rotate if it expires)

**Do not configure this on the day of App Store submission.**

### Auth patterns

| Pattern | When to use |
|---------|-------------|
| Email + password | Universal fallback; highest friction |
| Magic link (email) | Lower friction than password; good for B2B or low-frequency apps |
| Google Sign-In | Good conversion lift; easy with Firebase or Supabase; required to offer Apple alongside on iOS |
| Apple Sign-In | Required on iOS if any other third-party login is offered; privacy-friendly (hides email) |
| Phone number (OTP) | Consumer apps with anonymous/casual sign-up; high conversion, low friction |
| Anonymous auth | Allow users to use the app before signing up; convert to permanent account later. Firebase supports this natively. |

---

## Push notifications

Push notifications are more work than they appear. The happy path is easy; the edge cases are where time goes.

### The infrastructure

**APNs (Apple Push Notification service)** — Apple's delivery system for iOS. **FCM (Firebase Cloud Messaging)** — Google's delivery system for Android, also supports iOS.

Most indie apps use FCM for both platforms — it wraps APNs on iOS and handles Android directly.

**Expo Notifications** (for Expo apps): Manages FCM/APNs credentials, provides a unified SDK, and offers Expo's own push service as a proxy. The simplest option for Expo apps — removes credential management from the builder.

### What trips people up

**Permission request timing**: iOS requires an explicit permission request before showing push notifications. Android 13+ requires the same. Apps that prompt on first launch before showing any value have low opt-in rates. Best practice: prompt after the user has experienced core value (completed a task, set up their profile, received their first piece of relevant content).

**Background fetch vs. push**: If the app needs to refresh data in the background even when the user doesn't open a notification, that's a separate system — Background App Refresh (iOS) or WorkManager (Android). These are not the same as push notifications.

**Deep linking from notifications**: When a user taps a notification, the app should navigate to the relevant content — not just open to the home screen. This requires configuring notification handling in the foreground, background, and "killed" app states. Each state has different behaviour and requires separate code paths.

**Silent / data-only notifications**: Used to trigger a background refresh without showing a banner. Require the "Background Modes > Remote notifications" capability on iOS and careful handling to avoid triggering the "notification shown" path.

### What to build first

For v1: simple notification delivery (a user does X → send a push). Don't build notification preferences, quiet hours, or notification grouping at v1 unless they are core to the product.

---

## Common indie-scale architecture patterns

### "The personal tool"

- Local storage only (SQLite via Expo SQLite or Core Data)
- iCloud sync if iOS-only
- No server, no accounts
- Examples: Day One, Bear (v1), Things (v1), personal finance apps

### "The social consumer app"

- Firebase (Firestore + Auth + Storage + FCM)
- Push notifications via Expo Notifications or direct FCM
- Moderation queue (usually manual at first, automated later)
- Examples: Most consumer social apps at launch

### "The productivity SaaS"

- Supabase (Postgres + Auth + Storage)
- Subscription billing (RevenueCat — see monetization-strategy)
- Email notifications (Resend or SendGrid)
- Optional: Edge Functions for server-side logic
- Examples: Structured, Camo, Remote Year

### "The content + subscription app"

- Firebase or Supabase for user data
- RevenueCat for subscription management
- CDN-hosted content (Cloudflare R2, AWS S3)
- Push notifications for content releases
- Examples: Calm, Headspace at indie scale

---

## What to defer

Most indie apps don't need these at v1. Add them when you have a specific reason:

- **A/B testing infrastructure** — Validate the core experience first. Firebase Remote Config is fine when you need it.
- **Custom analytics pipeline** — Mixpanel, Amplitude, or PostHog are good choices, but even the free tier of Firebase Analytics will tell you what you need for the first 6 months.
- **Multi-region deployment** — One region is fine until users in a specific geography report latency problems.
- **Caching layer (Redis)** — Add when you have a measured performance problem, not before.
- **Microservices** — A single service is always the right starting point for indie scale.
