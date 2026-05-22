---
name: monetization-strategy
description: >-
  This skill should be used when the user needs to choose a revenue model or think through
  pricing before building payment infrastructure. Trigger on: "how should I charge for this",
  "subscription vs one-time purchase", "should I use IAP", "freemium model", "how do I price
  my app", "App Store pricing", "RevenueCat", "in-app purchases", "free trial", "how do I
  make money from this app", "monetisation strategy", or any question about revenue model,
  pricing tiers, or app store economics.
---

# Monetization Strategy

Help the builder choose a **revenue model before they build payment infrastructure** — and avoid the most common mismatch: a monetisation model that fights the app's natural use pattern.

The monetisation model isn't just a business decision. It shapes the UX deeply. A subscription app needs retention loops to justify recurring charges. An IAP app needs progressive value reveals to motivate purchases. A one-time purchase app needs to justify the upfront cost to a first-time visitor who hasn't used it yet. Getting the model wrong means rebuilding core UX later, not just swapping a payment screen.

## Operating mode: Socratic, use-pattern first

Don't recommend a model on the first message. The right model depends heavily on how the app is used. Ask first:

1. **What does the user do in this app, and how often?** Daily (habit tracker, notes, fitness) → recurring value → subscription fits. Monthly or infrequently (tax tool, travel planner, one-off utility) → subscription feels extractive → one-time or IAP fits better.
2. **What does the user get from paying?** Access to the full app? A specific feature? Consumable content? Virtual items? Premium content? The nature of what they're buying determines which model is structurally correct.
3. **Who is the user?** Consumer with personal use → price-sensitive, high churn risk. Professional using this for work → can justify higher subscription cost, churns less. Enterprise buyer → different model entirely (volume licensing, not App Store).
4. **What is the competitive landscape?** If every comparable app is free, charging anything upfront will reduce installs significantly. If comparable apps charge $4.99/month, that's market evidence that users will pay.
5. **What stage is the product at?** Pre-validation → start free, validate retention before charging. Post-validation, growing → time to add monetisation. Mature → optimise pricing, not model.

Only after these answers are clear — propose one model with an honest assessment of its failure mode for this specific app. Don't list all five models as equally valid.

## The model decision

### Subscription

**Fits when**: the app provides ongoing, recurring value — productivity tools, fitness tracking, meditation, language learning, professional tools, anything where using it this week makes the user want to use it next week.

**Revenue pattern**: Monthly or annual recurring revenue. Predictable but requires retention to be healthy. Churn is the enemy — if users subscribe for one month and leave, the economics don't work.

**What subscriptions demand from the UX**:
- A clear habit loop — the app must be part of the user's regular routine, or they'll cancel
- Enough perceived value that the renewal feels justified every month
- A retention mechanism for users who haven't opened the app in 10 days (push notification, email, in-app nudge)
- A win-back strategy for lapsed users

**Common failure mode**: Building a subscription app on top of a one-time-use product. If users only need the app once (complete a resume, plan a trip, file taxes), they'll subscribe, complete the task, and cancel. Monthly churn of 30–40% is fatal — the economics require < 5% monthly churn to be viable.

**Free trial**: Standard expectation for subscription apps. 7-day trials are common for daily-use apps. 14–30 days for lower-frequency or higher-priced apps. Apple supports introductory offers (free trial, discounted first period, pay-up-front discounts). Use them — trials dramatically reduce the barrier to subscription.

### One-time purchase (paid upfront / premium)

**Fits when**: the app delivers a complete, self-contained product with a clear value proposition that a user can evaluate before downloading — games, professional tools with a known price point, utilities with obvious utility.

**Revenue pattern**: One-time payment at download. Simple to explain to users. No ongoing relationship obligations. Dying as a model in the consumer App Store (free with subscriptions has displaced most of the paid-upfront market) but still viable for professional or niche tools where users expect to pay once.

**What paid apps demand from the marketing**:
- The App Store listing must justify the price to a stranger who has never used the app. Screenshots, description, and ratings all carry more weight than in a free app.
- No conversion funnel — the user either buys or doesn't. There's no free tier to hook them and convert later.
- Word of mouth and press coverage are disproportionately important because there's no "try before you buy"

**Common failure mode**: Underpricing out of fear. A $2.99 app that delivers $50 of value and could be a $9.99 app loses significant revenue and attracts users who expect disposable-quality software. If the app is good, price it accordingly.

### In-app purchases (IAP) — non-consumable

**Fits when**: the app has a meaningful free tier with premium features unlockable by purchase — photo editing tools, note apps with advanced features, professional tools where the free version is genuinely useful but limited.

**Revenue pattern**: One-time purchase of a specific feature or feature set. Simple for users to understand ("buy once, keep forever"). Can coexist with a free base app.

**What non-consumable IAP demands**:
- The free tier must be genuinely useful — not artificially crippled to force a purchase. Users can tell the difference and it creates resentment.
- The premium features must be clearly desirable — not arbitrary gate-keeping of basic functionality.
- The purchase decision is permanent — there's no monthly churn pressure, but there's also no monthly revenue either.

### In-app purchases (IAP) — consumable

**Fits when**: users buy something they use up — credits, coins, energy, extra generations, premium content downloads. Common in games, AI-powered apps (generation credits), and content apps.

**Revenue pattern**: Variable, non-recurring. Revenue depends on engagement and how fast users consume what they buy. High revenue ceiling from "whale" users; very low or zero revenue from most users.

**What consumable IAP demands**:
- Careful balance — the consumption rate and price need to feel fair. Users who feel they're being squeezed stop spending.
- The free allowance must be enough to hook users on the core loop before they hit a paywall. Apps that run out of free credits in 3 minutes before the user understands what they're buying have terrible conversion.
- Avoid whale dependency — if 5% of users generate 80% of revenue, you have a fragile business.

**Common failure mode**: Building an IAP economy before validating that users want the core product. Credits and coins are complex to balance and feel extractive if the product underneath doesn't justify them.

### Freemium (free + subscription)

**Fits when**: the app serves a broad audience with diverse needs — some casual, some power users. The free tier handles casual use; the paid tier unlocks professional-grade capabilities. Notion, Duolingo, Spotify.

**Revenue pattern**: Free users generate no revenue but provide scale, word of mouth, and conversion pipeline. Paid users generate recurring revenue. The ratio matters — if fewer than 2–5% of free users convert, the model struggles unless free users are very numerous.

**What freemium demands**:
- A free tier that's genuinely useful and acquires users at scale (freemium only works with volume)
- A paywall that converts — the premium features must be desirable enough that a meaningful fraction of users pays for them
- Analytics to understand where users hit the paywall and whether they convert or churn at that point

**Common failure mode**: Giving away too much for free (no incentive to upgrade) or too little (free tier isn't useful enough to attract users). Finding the right paywall placement is an iterative, data-driven process — plan for multiple experiments.

### Advertising

**Fits when**: very high volume, content consumption apps where interruptions are acceptable — casual games, news readers, entertainment apps. Usually not appropriate for productivity, professional, or utility apps.

**Revenue pattern**: CPM / CPC revenue from ad networks (Google AdMob, Unity Ads for games, Meta Audience Network). Revenue is low per user — typically $0.5–$5 RPM (revenue per 1,000 impressions) depending on audience and format.

**Common failure mode**: Ad monetisation on a low-volume app. An app with 10,000 DAU generating $2 CPM earns roughly $20/day. Ads only make economic sense at scale or when combined with a premium tier that lets users pay to remove ads.

## The revenue model shapes the UX

This is the point builders most often miss:

| Model | UX implication |
|-------|----------------|
| Subscription | Needs habit loop, retention nudges, and offboarding friction (cancellation flow) |
| One-time purchase | App Store listing carries the full sales burden; onboarding must deliver perceived value fast |
| Non-consumable IAP | Free tier must be genuinely useful; paywall placement is a product decision, not a business one |
| Consumable IAP | Core loop must be addictive and satisfying before users hit the credit ceiling |
| Freemium | Volume matters; paywall placement must be tuned; analytics from day one |
| Advertising | User session length and return frequency must be high; ad placement must not destroy the UX |

## App Store mechanics

Apple's 30% commission applies to all in-app purchases and subscriptions. The 15% rate (Small Business Program) applies if your App Store revenue was under $1M in the previous calendar year — most indie apps qualify.

Google Play has equivalent tiered rates.

This affects pricing: a subscription priced at $9.99/month nets the developer $7 (at 30%) or $8.50 (at 15%). Factor this into unit economics before setting price.

See [app-store-economics.md](../../references/monetization-strategy/app-store-economics.md) for the full breakdown of commission structures, pricing tiers, introductory offers, and revenue reporting.

See [monetization-models.md](../../references/monetization-strategy/monetization-models.md) for the detailed model comparison with failure modes per model.

## RevenueCat

For apps using subscriptions or IAP: **RevenueCat** is the near-universal recommendation for indie developers. It handles:
- Receipt validation on both iOS and Android
- Subscription status tracking across platforms
- Entitlement management (what features is this user allowed to access?)
- Subscription analytics (MRR, churn, LTV, trial conversion)
- Paywalls (including no-code paywall builders)
- Webhook integrations to your backend

The free tier covers up to $2,500 MRR. Worth adding from day one even if you're not charging yet — it gives you the analytics infrastructure you'll want later.

## What to avoid

- **Recommending a model without understanding the use pattern.** Subscriptions on one-time-use apps and one-time purchases on daily-use apps are both wrong for structural reasons.
- **Defaulting to "freemium" as the safe answer.** Freemium requires volume. Without significant scale, it's just "give it away for free and hope."
- **Setting prices out of fear.** Underpricing is a real problem. Users signal quality through price — a well-built app priced at $0.99 is treated as disposable.
- **Skipping the economics.** Help the builder think through: what is the revenue at 1,000 paying users? What would they need to cover their costs and time?

## Handoffs

- Model chosen, now needs subscription or IAP infrastructure → [technical-architecture](../technical-architecture/technical-architecture.md) (RevenueCat, backend for entitlements)
- Paywall placement and UX → [ux-interaction-design](../ux-interaction-design/ux-interaction-design.md)
- Pricing and positioning relative to competitors → [market-research](../market-research/market-research.md)
- App Store listing to support the revenue model → [onboarding-and-documentation](../onboarding-and-documentation/onboarding-and-documentation.md)
