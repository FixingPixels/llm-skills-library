# App Store Economics

Reference for Apple App Store and Google Play commission structures, pricing mechanics, introductory offers, subscription revenue reporting, and review solicitation timing. Use when helping a builder set prices or understand the financial mechanics of app distribution.

> **Verify current rates before pricing decisions.** Commission percentages, Small Business Program thresholds, developer-account fees, and price tier ladders are policy details that change. Treat the figures below as a structural guide, not a live quote — confirm with Apple's and Google's current developer documentation before the builder commits to a price.

---

## Commission structure

### Apple App Store

**Standard rate: 30%**

Applies to:
- One-time purchases (paid apps and non-consumable IAP)
- Consumable IAP
- First year of any subscription
- Auto-renewable subscriptions from users who have subscribed to the app for less than 12 months

**Reduced rate: 15%**

Applies to:
- Auto-renewable subscriptions **after a subscriber has maintained an active subscription for 12 consecutive months** — the rate drops to 15% for that subscriber, going forward, automatically
- All revenue for developers enrolled in the **App Store Small Business Program**

### App Store Small Business Program

Developers who earned less than **$1,000,000 in App Store proceeds** in the prior calendar year are eligible. Enrollment is annual and must be actively maintained.

At the 15% rate: a $9.99/month subscription nets the developer **$8.49/month** per subscriber (vs. $6.99 at 30%).

**Implication for pricing**: If you qualify for the Small Business Program, factor the 15% rate into your unit economics — not 30%. Most indie developers qualify.

### Google Play

Google Play has moved to a similar tiered structure:
- **15% on the first $1M USD** of annual developer revenue (applicable to all developers, not just small ones)
- **30%** on revenue above $1M/year

For subscriptions, Google Play also offers a reduced 15% rate after 12 months of continuous subscription per user.

**Net effect**: For most indie developers (under $1M/year), effective commission is 15% on both platforms. Factor this into pricing decisions.

---

## Pricing tiers

### How pricing tiers work

Apple and Google do not allow arbitrary price points. Apps and IAP must be priced at specific "tiers" — predefined price points in each currency. The stores handle currency conversion and localisation automatically.

**Common USD price points**:
`$0.99 / $1.99 / $2.99 / $3.99 / $4.99 / $5.99 / $6.99 / $7.99 / $8.99 / $9.99 / $12.99 / $14.99 / $19.99 / $24.99 / $29.99 / $49.99 / $99.99`

Price points outside these tiers are not directly available — you must choose the nearest tier or use custom pricing (available in some regions with limitations).

### Pricing psychology at common tiers

**$0.99**: Often signals low quality or impulse purchase. Appropriate for narrow utilities, add-ons, or aggressive initial pricing. Not appropriate for professional tools.

**$2.99–$4.99**: The "considered purchase" range. Users evaluate before buying but the friction is low. Works for solid utilities and mid-tier tools.

**$9.99**: Strong psychological anchor — "under $10." Feels like the right price for a quality app. One of the most common subscription price points.

**$14.99–$19.99/month**: Appropriate for professional tools with clear productivity ROI. B2B-adjacent apps can support this.

**Annual pricing**: Typically offered at the equivalent of 9–10 monthly payments (a 16–25% discount vs. monthly). Apple and Google both support annual subscriptions natively.

### Localised pricing

Apple automatically converts USD prices to local currencies at approximate purchasing power parity — but the conversion is not always generous to developers in high-purchasing-power markets. Review localised pricing before launch, especially for markets where the app has significant potential.

Apple introduced **custom pricing by territory** — developers can override the default conversion for specific markets. Worth using if the app has a significant audience in markets where auto-conversion underprices the app.

---

## Subscription mechanics

### Subscription periods

Apple supports: weekly, monthly, 2-month, 3-month, 6-month, annual.

Most apps use: **monthly** (lower barrier, lower LTV) and **annual** (higher LTV, lower churn).

### Introductory offers

Apple supports three types of introductory pricing for new subscribers:

1. **Free trial**: Access for a period (7, 14, 30 days) before the first charge. User must have a payment method on file. Most common introductory offer.
2. **Pay as you go**: Discounted price for a set number of billing periods before full price. (e.g., $0.99/month for 3 months, then $9.99/month)
3. **Pay upfront**: Discounted one-time payment covering a set period before transitioning to recurring. (e.g., $9.99 for 3 months, then $9.99/month)

**Only one introductory offer per subscriber**. Once a user has used an introductory offer for a product group, they can't get another one for any product in that group.

### Grace period and billing retry

If a subscriber's payment fails (expired card, insufficient funds), Apple retries for up to 60 days — this is the **billing retry period**. During this time the subscription is considered "in billing retry" — the developer can optionally continue providing access or lock the user out.

**Billing grace period**: A separate opt-in feature where Apple provides up to 16 days of continued access while retrying — reduces involuntary churn. Enable this in App Store Connect; it's free to use and measurably reduces churn.

### Subscription groups

Subscriptions belong to a subscription group. Users can only subscribe to one product within a group at a time — switching between monthly and annual within a group is an upgrade/downgrade, not a cancellation and resubscription.

Organise all tiers of your subscription (monthly, annual, family, etc.) into a single group. Different product lines (e.g., a premium add-on vs. the core subscription) can live in separate groups.

---

## Review and rating solicitation timing

Apple requires apps to use the native `SKStoreReviewController` / `requestReview()` API — no custom review prompts. This limits you to requesting a review, not controlling the exact timing of when Apple shows the dialog.

**Apple enforces**:
- The system dialog can appear at most **3 times per year per app**
- Apple may suppress the request if the user has already rated the app
- Apple controls whether the dialog actually shows — your `requestReview()` call is advisory, not guaranteed

**Optimal timing**:
- After a user has completed a clear success (finished a task, hit a milestone, completed a level) — not immediately after launch
- For subscription apps: **not immediately before or after billing** — users who just renewed don't need prompting; users who just failed a payment are in a bad moment for a review request
- After the user has had enough time to form a genuine opinion — typically 3–7 uses for a daily-use app

**Avoid**:
- Requesting review immediately on first launch
- Requesting review after a negative in-app event (error, failed sync, empty state)
- Requesting review mid-task

---

## Revenue reporting in App Store Connect

### Proceeds vs. sales

App Store Connect reports show two figures:
- **Sales**: Total retail price charged to the user
- **Proceeds**: What the developer receives after Apple's commission

Always calculate unit economics on **proceeds**, not sales. A $9.99 subscription generates $8.49 in proceeds (at 15%) or $6.99 (at 30%) — not $9.99.

### Reporting lag

App Store Connect revenue reporting has approximately a **24–48 hour lag**. Subscription events (new subscriptions, cancellations, billing retries, refunds) don't appear in real time.

**RevenueCat** provides near-real-time subscription analytics with more granularity than App Store Connect natively — cohort analysis, LTV, churn by acquisition channel, trial conversion. Worth using from day one even on the free tier.

### Refunds

Apple processes refunds directly. The developer has no control over whether a refund is granted — Apple makes the decision and notifies the developer via a notification in App Store Connect. Refund rates above 5% attract attention and can trigger App Store review.

---

## The Small Business Program in practice

Eligibility check: Did your app (and all apps under your developer account) earn less than $1,000,000 in App Store proceeds in the prior calendar year?

If yes:
- Enroll at appstoreconnect.apple.com → Agreements, Tax, and Banking
- The 15% rate applies to all your revenue in the current calendar year
- If you exceed $1M during the year, the rate reverts to 30% for the remainder of that year
- Re-enroll annually if eligible

The $350,000/year in additional proceeds (the difference between 15% and 30% on $1M of revenue) is meaningful — don't overlook enrollment.

---

## Quick reference: What does it actually cost?

| Subscription price | Commission | Proceeds/month |
|--------------------|-----------|----------------|
| $4.99/month | 15% (SBP) | $4.24 |
| $4.99/month | 30% (standard) | $3.49 |
| $9.99/month | 15% (SBP) | $8.49 |
| $9.99/month | 30% (standard) | $6.99 |
| $14.99/month | 15% (SBP) | $12.74 |
| $99.99/year | 15% (SBP) | $84.99 |
| $99.99/year | 30% (standard) | $69.99 |

Use proceeds, not sales, in every revenue projection.
