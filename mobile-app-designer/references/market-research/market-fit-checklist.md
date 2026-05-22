# Market Fit Checklist

Run this when a developer wants a structured read on whether their app has a market, where it lives, and what it's competing with.

## Step 1: Name the comparison set (5-10 apps)

Without 5+ comparison apps, no market analysis is reliable. If the developer can't name them:

- They haven't used enough apps in their target category.
- The space may be more crowded than they realize.
- They're at risk of building something that already exists, badly.

Push for: 3 close comparisons (same category, similar feature scope, similar audience), 2-3 adjacent (same audience but different approach, or same approach for a different audience), 1-2 aspirational (the best apps in the space, even if they're large teams).

The comparison set must come from direct App Store research — not just "I think X is a competitor." The developer should have downloaded each one and used it.

## Step 2: Position on the four axes

For each comparable, place the app on:

- **Complexity** (single-job minimal → feature-rich power tool)
- **Session model** (glance/widget → daily check-in → deep work session)
- **Monetization model** (free → freemium → one-time purchase → subscription)
- **Platform stance** (iOS-only → Android-only → cross-platform)

Where does the developer's app sit relative to comparables? If it sits *exactly* where one of them does, the design needs a sharper differentiator. If it sits in a gap, that's interesting — investigate why no one is in that gap (often there's a reason: no monetization model, audience too small, too expensive to build).

## Step 3: Differentiator audit

The developer should be able to answer:

- **What's the one thing this does that no comparable does?**
- **Why hasn't a well-funded team done it already?** (Honest answer: it's risky, the audience is small, it requires specialized knowledge, or… it's been done and you don't know.)
- **Is the differentiator visible at the App Store listing level?** A differentiator visible in the title, subtitle, or first screenshot is far stronger than one buried inside the app.

If the only differentiator is "better design" or "less cluttered UI," that is not a market position. Every app claims this. The market doesn't reward incremental polish unless distribution is solved.

## Step 4: Audience size sanity check

For the target audience, rough estimates:

- **Mass-market utility / social** — millions of potential users, but top-of-chart apps are entrenched. New entrant needs category-creation or a viral loop to break in.
- **Niche productivity or lifestyle** — hundreds of thousands of potential users. Sustainable at indie scale if positioned well and monetization is right.
- **Professional vertical tool** (e.g. nurses, real estate agents, contractors) — tens to hundreds of thousands of potential users, higher willingness to pay, lower organic App Store discoverability.
- **Hyper-niche or hobbyist** — thousands to tens of thousands. Can be very loyal and willing to pay; revenue ceiling is real but may be acceptable for a solo developer.

The developer's expectations should match the audience size. A hyper-niche tool won't support a subscription business at scale. A mass-market app can, but requires a marketing budget that most solo developers don't have.

## Step 5: Monetization / unit economics sanity check

Match the audience and use pattern to the monetization model:

- A **daily-habit app** (habit tracking, journaling, language learning) can support a subscription; users see continuous value. But churn after year 1 is high — plan for it.
- A **single-job utility** (unit converter, noise meter, flashlight) almost never supports a subscription. One-time purchase or free-with-tip-jar is the right model.
- A **professional vertical tool** can support a higher subscription price ($10-30/month) if the ROI for the professional is clear.
- An **ad-supported app** requires very high daily active users to generate meaningful revenue for a solo developer. Most solo apps should not default to this model.

If the developer's monetization model doesn't match their audience's use pattern and willingness to pay, flag it now. Revenue projections built on wrong assumptions are worse than no projections.

For a full treatment of monetization options, hand off to [monetization-strategy](../../skills/monetization-strategy/monetization-strategy.md).

## Step 6: Distribution path

How will the app reach users?

- **Organic App Store search (ASO)** — viable for niche apps where users have high search intent. Requires keyword research, strong ratings, and a category where search volume exists for the problem.
- **Content marketing / SEO** — blog, YouTube, or newsletter-first strategy. Builds trust and audience before launch. Longer timeline but more durable.
- **Social media / community** — launch into an existing community (subreddit, Discord, niche forum) that already has the problem. Fast feedback, potentially fast initial users.
- **Product Hunt / press** — produces a launch spike, rarely produces sustained growth. Useful for credibility and initial reviews, not a distribution strategy.
- **Paid user acquisition (UAC, Meta ads)** — requires positive LTV/CAC ratio before scaling. Most solo developers are not in that position at launch.
- **Word of mouth** — happens when the app creates a story worth telling or a visible output (a chart, a streak, a completion certificate) users share. Design for shareability if this is the intended channel.

The right distribution path depends on the developer's skills and network. Solo developers often default to "launch on Product Hunt and post on Twitter" without understanding that sustainable growth requires a repeatable acquisition channel.

## Step 7: Honest verdict

After steps 1-6, ask:

- **Is the audience real?** Specific. "Productivity users" isn't real; "remote workers who want a one-tap daily standup logger" might be.
- **Is the differentiator strong enough to get discovered?** Or is the developer building a "me-too" that needs paid acquisition or a pre-existing audience to gain any traction?
- **Does the monetization model match the use pattern and audience size?**
- **Is the distribution path realistic for the developer's actual resources and network?**

If 3+ of these are no, the developer has work to do — not necessarily on the product, but on the framing, the audience definition, or the distribution strategy.

## Red flags to surface honestly

- Developer can't name 5 competitor apps they've actually used.
- Developer believes "no one has built this."
- Developer's pitch leads with features, not with the user's problem.
- Developer expects organic App Store growth without a launch plan or marketing strategy.
- Developer is building for "everyone" — no specific user, context, or job.
- Developer hasn't spent 2+ weeks living inside their competitor apps before starting to build.
- Developer's target audience is themselves and their immediate circle — useful for validation, insufficient as evidence of market demand.
- Developer chose the monetization model without checking whether the audience's session pattern supports it.

These aren't disqualifying — they're signals that more market work is needed before the build gets further.

## App Store research checklist

When reviewing competitor apps, push the developer to note:

- **Category rank** — where is it sitting in the category charts? Stable or trending?
- **Rating and review volume** — star rating matters for conversion. What do 1-star and 5-star reviews each say? The 1-stars often contain the gap.
- **Last update date** — an app with strong ratings and recent updates is an active competitor. An app with strong ratings but no update in 18 months may be an acquisition target or a gap opportunity.
- **Screenshots and description** — what job are they claiming to do? How are they positioning? What keywords appear in their title/subtitle?
- **Pricing** — free, freemium, one-time, subscription? What tier?
- **App size** — relevant for offline-capable apps; users are sensitive to large downloads.

Systematic review of the top 5-10 apps in the target category before building is the single most valuable market research step a solo developer can take.
