# Monetization Models

Detailed breakdown of each revenue model with fit criteria, mechanics, failure modes, and real examples. Use to evaluate which model fits a specific app's use pattern — not to present all models as equally valid options.

---

## Subscription

### Mechanics

User pays a recurring fee (monthly or annual) for continued access. Payment is processed automatically by the App Store; the developer's backend (or RevenueCat) tracks subscription status and controls feature access via entitlements.

### Economic profile

- **Revenue type**: Recurring (predictable)
- **Unit economics**: LTV = ARPU × (1 / monthly churn rate). A $9.99/month app with 3% monthly churn has an expected LTV of ~$333 per subscriber.
- **Healthy churn range**: < 3% monthly (consumer); < 1% monthly (professional tools)
- **Breakeven**: Customer acquisition cost (CAC) must be less than LTV × gross margin

### When it fits

- App used **daily or weekly** — the habit is the justification for recurring payment
- App delivers ongoing value that grows over time (more content, more data, more features)
- Users are professionals who will expense the cost or see clear ROI from use
- Comparable apps in the category charge subscriptions — users expect it

### When it doesn't fit

- App with a clear end-state (file a tax return, build a resume, plan one trip) — users complete the task and cancel
- App used fewer than a few times per month — infrequent users do the mental math and cancel
- Commodity utility with free alternatives — unless the experience is clearly premium, users resent paying monthly

### Common failure modes

**High first-month churn**: Users subscribe, explore, don't build a habit, and cancel before the second charge. Indicator: 30-day cancellation rate > 50%. Root cause: the value isn't sticky, or the habit loop isn't established during the trial.

**Trial-to-paid conversion below ~30%**: Trial is working (users start it) but not converting. Indicator: look at what users do during the trial — do they reach the core value? Are they hitting a paywall before they understand what they're paying for?

**Annual vs. monthly ratio below 20%**: Annual subscribers churn at far lower rates and have higher LTV. An app where most users are on monthly plans has fragile revenue. Incentivize annual with a discount (typically 30–40% off equivalent monthly).

### Real examples

- **Duolingo Plus**: Adds offline mode, removes ads. The free tier is the product; Plus removes friction. Subscription justified by daily habit.
- **Headspace / Calm**: Full content library behind subscription. Single-purpose enough that there's no free alternative to the core content.
- **Bear / Ulysses**: Professional writing tools with monthly/annual subscriptions. Users are professionals who use them daily; the subscription is justifiable.

---

## One-time purchase (premium paid app)

### Mechanics

User pays at download. No recurring billing. Full feature access post-purchase. No free tier — the App Store listing converts the sale.

### Economic profile

- **Revenue type**: Non-recurring (transactional)
- **LTV**: Equal to the purchase price minus the App Store commission (30% or 15%)
- **Growth model**: Volume × price. Revenue is directly proportional to new downloads — no compounding from retained subscribers.

### When it fits

- App delivers a **complete, discrete product** — a game, a professional tool with a known genre, a utility with obvious utility
- Users expect to pay once — professional tools, creative software, games
- The App Store listing (screenshots, description) can clearly convey what the user gets
- Category has a history of paid apps — the pricing convention exists

### When it doesn't fit

- Content apps (the content changes; users want access, not a permanent license to old content)
- Apps where the value grows over time — users may feel they paid for a product that's now outdated
- Broad consumer apps competing with free alternatives

### Common failure modes

**Underpricing**: Fear of rejection leads builders to price at $0.99 or $1.99. Users assume low price = low quality. Apps in professional or creative categories that charge < $4.99 often see lower conversion than equivalent apps at $9.99+. Test higher prices.

**Invisible discovery**: Paid apps don't appear in "top free" charts. App Store search is crowded. Without word-of-mouth, press, or paid acquisition, a paid app can be invisible. The marketing plan matters more here than for free apps.

**No upsell path**: If the app is a one-time purchase, there's no path to additional revenue from existing users. Future major versions are often sold as separate apps (the "2" strategy) to re-monetise the user base.

### Real examples

- **Procreate**: $12.99 one-time, one of the highest-grossing paid iPad apps. Professional tool; users know what they're buying.
- **CARROT Weather**: One-time purchase (with an optional subscription for premium features). Works because the core product is complete.
- **Patterned**: One-time purchase creative tools in a niche professional category.

---

## In-app purchases — non-consumable (unlock)

### Mechanics

App is free to download. Specific features or content are locked behind a one-time in-app purchase. Once purchased, the user owns that item permanently — it syncs across the user's devices via the App Store.

### Economic profile

- **Revenue type**: Non-recurring, per-feature
- **Conversion rate**: Typically 1–5% of free users purchase, depending on paywall quality and feature desirability
- **LTV**: Purchase price per item × number of items purchased

### When it fits

- App has a **meaningful free tier** — not crippled, but naturally limited
- The premium features are clearly desirable to a subset of users
- Users can evaluate the free tier and decide if the unlock is worth it
- The app serves both casual users (who never pay) and power users (who happily pay for more capability)

### Common failure modes

**Free tier is too limited**: Users download the app, hit the paywall immediately, and leave without understanding what they're buying. The free experience must have enough value that users are invested before they see the unlock prompt.

**Free tier is too generous**: No compelling reason to upgrade. The unlock must offer features that a meaningful percentage of users genuinely want. If conversion is under 1%, either the free tier is too complete or the premium features aren't desirable enough.

**Non-obvious restore mechanism**: Apple requires that non-consumable purchases be restorable on new devices or after reinstall. "Restore Purchases" must be accessible in the UI. Missing this causes support headaches and, in some cases, App Store rejection.

### Real examples

- **GoodLinks**: Free to download; full features available after a one-time unlock. Works because the app is genuinely useful free and clearly better paid.
- **Darkroom**: Subset of professional editing tools are free; advanced tools require a purchase or subscription. Well-executed two-tier model.

---

## In-app purchases — consumable (credits / coins)

### Mechanics

User buys an item that is "consumed" by use — credits, coins, tokens, energy, generation credits. When depleted, the user buys more. Apple and Google do not require restore functionality for consumables (unlike non-consumables).

### Economic profile

- **Revenue type**: Variable, usage-driven
- **Revenue ceiling**: High — power users can spend many multiples of a subscription price
- **Revenue floor**: Very low — most users spend nothing beyond the initial free allocation
- **LTV distribution**: Highly skewed — a small number of high-spenders drive a disproportionate share of revenue

### When it fits

- Apps with a **natural consumption loop** — AI image generation (generate credits), games (energy, coins, keys), translation apps (character credits), voice apps (minute credits)
- The free allocation is enough to hook users on the core value before they run out
- The consumption rate feels natural and fair (users don't feel squeezed)

### Common failure modes

**Too short a free runway**: Users run out of credits in the first session before they understand the value. Conversion is low because they haven't formed an attachment to the product. Solution: be generous with the free allocation, even at the cost of short-term revenue.

**Whale dependency**: If 5% of users generate 80% of revenue, the business is fragile — those users churn, change their spending habits, or get acquired by a competitor's promotion. Healthy consumable economies have broader spending distributions.

**Feeling like a casino**: Consumable IAP economies can feel extractive if not carefully balanced. Users who feel manipulated leave and write negative reviews. Transparent pricing ("$2.99 for 100 credits, one image = 5 credits") builds trust; opaque economies ("premium currency" with no clear exchange rate) erodes it.

### Real examples

- **DALL-E / Midjourney (mobile)**: Generation credits — each image costs credits; users buy more when they run out.
- **Duolingo** (historically): Hearts as a consumable energy system. Controversial — users perceived it as punitive. Duolingo has modified this system significantly in response to user feedback. A cautionary example of consumable balance going wrong.
- **Most casual games**: Coins, gems, energy, keys — extensive literature on what works and what feels extractive.

---

## Freemium (free + subscription)

### Mechanics

App is free with a baseline feature set. Advanced features are locked behind a subscription. The free tier is the acquisition channel; the subscription is the revenue model.

### Economic profile

- **Free-to-paid conversion**: Typically 2–10% of free users
- **Revenue model**: Subscription revenue from the paid tier
- **Volume requirement**: Because only 2–10% pay, freemium needs large free user numbers to generate meaningful subscription revenue. At 5% conversion and $7.99/month, you need 1,000 paying users (~20,000 free users) to reach $8K MRR.

### When it fits

- App can serve casual users meaningfully for free while offering professional-grade features at a price
- The builder can acquire free users at low cost (organic, viral, SEO, word of mouth)
- The paywall can be tuned — there's analytics to understand where users hit it and whether they convert

### Common failure modes

**Freemium with insufficient volume**: Freemium only works with scale. A solo developer who can't drive thousands of free users shouldn't rely on freemium — direct subscription or one-time purchase is more viable at low volume.

**Paywall in the wrong place**: Paywalling features before users understand why they want them → low conversion. Paywalling after users have invested significantly → resentment. Finding the right moment is iterative.

**Features too similar across tiers**: If the free and paid tiers are nearly identical, there's no reason to upgrade. If the free tier is clearly crippled, it feels dishonest. The right gap is: "the free tier is genuinely useful for casual use; the paid tier is genuinely better for serious use."

---

## Advertising

### Mechanics

Revenue from showing ads — banner ads, interstitials, rewarded video — via networks like Google AdMob (most common), Unity Ads (games), Meta Audience Network.

### Economic profile

- **Revenue metric**: RPM (revenue per 1,000 impressions) or ARPU (average revenue per user per month)
- **Typical RPM**: $0.50–$5 for banners; $5–$20 for interstitials; $15–$40 for rewarded video — highly variable by audience, country, and market conditions
- **Volume requirement**: At $2 RPM, 1M impressions/month → $2,000/month. Ads require significant scale.

### When it fits

- Consumer apps with very high session frequency and daily active users
- Casual games, entertainment, content apps where interruptions are tolerable
- Combined with a "remove ads" paid tier — the ads create a reason to pay

### Common failure modes

**Ads on a low-volume app**: The math doesn't work. Ads are almost never the right primary model for indie apps with fewer than 100K MAU.

**Ads that destroy the UX**: Interstitials that block content, banners that cover controls, popups that interrupt core flows — these generate reviews that say "this app is riddled with ads" and increase churn. If ads are in the model, they must be placed where they're tolerable.

**Ad monetisation on a productivity or professional app**: Users paying attention to their finances, health, or work feel degraded by ads. The association damages the brand even if users tolerate the ads.
