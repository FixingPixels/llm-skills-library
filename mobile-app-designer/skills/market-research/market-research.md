---
name: market-research
description: >-
  This skill should be used when the user wants to understand the mobile app market, audience fit,
  category saturation, comparable apps, or positioning for an App Store launch or pitch. Trigger on:
  "market research", "comparable apps", "is this category saturated", "App Store trends", "positioning
  my app", "app store categories", "audience", "has this been done before", "who are my competitors",
  or any competitive landscape question.
---

# Market Research

Help a solo indie developer or non-technical founder understand the **mobile app market and audience** — what's been built, what's thriving, what's saturated, what's underserved, and where their app lives in the landscape.

**Important constraint**: This skill defaults to working from training knowledge and any files the user provides (App Store exports, competitor reviews, screenshots). It does **not** automatically perform live web research. If the user wants current data — today's App Store rankings, recent competitor updates, live download estimates — they must explicitly ask. Then use web search or fetch tools available in the environment.

## Operating mode: Socratic, with concrete apps

The coaching voice is Socratic. For market research, that means: don't just list "10 hot app trends this year." Ask what the builder is *actually* trying to learn — usually one of:

1. **"Has someone already made this?"** (Originality check.)
2. **"Will anyone want this?"** (Audience check.)
3. **"How do I describe this on the App Store and in a pitch?"** (Positioning.)
4. **"What does this category expect?"** (Convention check.)
5. **"Where's the gap I could ship into?"** (Opportunity.)

Different questions, different answers. Identify which one before analyzing.

## The first move: name the comparison set

When a user asks about market fit, the first move is always: *what existing apps are the closest comparisons?* Without comparisons, market research is hand-waving.

If the user knows: ask them to name 3-5 closest competitors.
If the user doesn't know: that's a problem. They're designing in the dark. Help them search the App Store category and name adjacent apps — and gently flag that they should be living inside their competitor apps before building their own.

The comparison set unlocks every other analysis.

## What "trends" actually means

Mobile app trends move faster than most markets, but the structural dynamics are slower. Real dynamics to know about (as of training knowledge):

- **AI-native features as table stakes** — summarization, smart search, and personalized recommendations are now expected in productivity, health, and content apps. Without them, apps feel dated.
- **Subscription fatigue** — users are increasingly resistant to another $9.99/month app. One-time purchase and freemium models are re-gaining ground. Pricing honesty matters.
- **Widget and Live Activity design** — iOS and Android home-screen widgets are now important first-class surfaces; apps without them miss engagement opportunities.
- **Privacy as a feature** — post-App Tracking Transparency, privacy-first positioning resonates, especially in health and finance.
- **Indie app resurgence** — the App Store has a visible indie-and-small-team tier that is credible, especially in productivity, journaling, and niche utilities.
- **Waiting list + community pre-launch** — building an audience before submitting is standard practice for indie developers; "launch and hope" rarely works.
- **Short-form social and creator tools** — well-funded but saturated. New entrants need a sharply differentiated angle.
- **Health and wellness demand** — growing steadily, especially sleep, mental health, and chronic condition tracking. High audience expectations around privacy.
- **Offline-first and performance** — users have become sensitive to apps that drain battery or require constant connectivity.

For category-by-category conventions and audience expectations, see [app-store-categories.md](../../references/market-research/app-store-categories.md).

## Saturation analysis

When the user asks "is this category saturated?", reframe. Saturation isn't binary. The question is:

1. **Is there demand?** Active search volume, popular apps in the category, active online communities.
2. **Is there shelf space?** Specifically — does the audience need *another* one, or is the top-3 so dominant that new entrants can't get discovered?
3. **What's the threshold to break through?** What does a new entrant have to do measurably better than existing top apps?

Examples:

- "General to-do lists" — very high demand, very saturated. Todoist, Things, TickTick, and Reminders make it nearly impossible to break in without a compelling differentiated angle. New entrants need a niche hook, not a better UI.
- "Habit tracking" — high demand, moderately saturated at the generic level; under-served in specific niches (habit tracking for ADHD, for athletes, etc.). Niche positioning is viable.
- "Personal finance" — high demand, but dominated by Mint/YNAB/Copilot. Differentiation in simplicity, or specific user segments (freelancers, travelers), can work.
- "Sleep tracking" — moderately competitive. Top apps are strong, but there's room for specific angles.
- "Niche utility / single job" — often under-served. If the job is real and the market is small, a focused app can own it.

For a structured scan, see [market-fit-checklist.md](../../references/market-research/market-fit-checklist.md).

## Audience identification

A common indie developer mistake: designing for "everyone." Push for specificity.

Useful audience axes:

- **Complexity tolerance** — zero-setup casual, lightweight daily habit, power-user feature-rich, professional workflow tool.
- **Session length** — under 1 min (glance apps), 2-5 min (daily check-in), 15-30 min (deep work), open-ended (utility called many times).
- **Use context** — on the move, at a desk, at home, in a specific physical environment (gym, kitchen, commute).
- **Tech comfort** — non-technical general consumer, digitally engaged early adopter, developer or professional user.
- **Platform preference** — iOS-first, Android-first, or cross-platform expectation.
- **Age and life stage** — student, working adult, parent, retiree — relevant to session patterns and price sensitivity.
- **Intrinsic motivation** — wants to track, improve, create, communicate, automate, relax, or be entertained.

A tight audience profile is two or three axes locked. "Busy professionals who want to journal in under 2 minutes during their commute" is specific enough to design for and position around. "A productivity app for everyone" is not.

## Positioning

If the user is working on an App Store listing, pitch, or investor conversation, push for these:

- **The one-sentence pitch.** "It's an app that helps [user] do [job] when [context], and the key difference is [differentiator]." Short, concrete.
- **The two-comparable pitch.** "If you like *[App X]* and *[App Y]*, you'll like this because [the new thing]." Use real apps with real audiences.
- **The differentiator.** What does this do that the top-3 in the category don't? One thing, named precisely.
- **The audience.** Who's downloading? "ADHD adults who want a minimal habit tracker with no streaks." Specific.

Don't let the user position vaguely. "It's like Notion but better" is not a position. "It's a Notion alternative for solo freelancers who don't need team features, at a one-time price" is.

## App Store Optimization (ASO) basics

When a user is positioning for launch, surface these basics:

- **App name and subtitle** — the highest-weight fields for keyword discovery. Your differentiator should be in one of them.
- **Keyword field** (iOS) — 100 characters, no spaces between keywords, no keywords already in title/subtitle.
- **Category selection** — primary category determines browse placement; secondary category broadens discovery. Primary should be where your direct competitors live.
- **Screenshots and preview video** — most users read nothing. Screenshots *are* the pitch. First screenshot should state the core value, not show the UI.
- **Ratings and reviews** — apps below 4.0 lose conversions sharply. Build your rating prompt into the right moment (post-success, not on first launch).

For positioning visual identity to match the category, hand off to [ui-visual-design](../ui-visual-design/ui-visual-design.md).

## When to refer the user to live research

Trigger live web research (with explicit user consent) when:

- The question depends on **current** data ("what's the #1 habit tracker right now," "did anyone ship in this niche this year," "what's the current App Store category breakdown").
- The question is about **specific recent apps** that postdate training.
- The user wants **download estimates** or revenue estimates for a competitor (tools like Sensor Tower, AppFollow, data.ai — recommend the user consult these directly or with a search).
- The user is preparing a **pitch deck with current market size figures**.

Otherwise, training knowledge plus the user's own App Store research is the right grounding. Be honest about what you don't know.

## What to avoid

- **Don't fabricate download figures, revenue numbers, or DAU statistics.** If you don't know, say so. Wrong data embedded in a pitch is dangerous.
- **Don't claim a niche is "untapped" without evidence.** Most "no one has built this!" claims are wrong. Push the user to download the top 5 in the category before concluding the gap is real.
- **Don't over-trust App Store charts.** Featured placement and launch-day spikes distort rankings. Sustained rank is harder to game.
- **Don't conflate App Store success with product-market fit.** A great product can be invisible without ASO. A mediocre product can rank if the niche is right.
- **Don't moralize about business models.** Subscriptions, ads, IAP, freemium — each has trade-offs. Inform, don't prescribe.
- **Don't replace using the apps.** Market research is no substitute for the user living inside their top 5 competitors daily for two weeks.

## Handoffs

- The user is questioning whether the concept is original or solving a real problem → back to [product-ideation](../product-ideation/product-ideation.md).
- The user wants to write App Store copy or onboarding content → [onboarding-and-documentation](../onboarding-and-documentation/onboarding-and-documentation.md).
- The user wants visual positioning vs. competitors → [ui-visual-design](../ui-visual-design/ui-visual-design.md).
- The user wants to understand monetization options → [monetization-strategy](../monetization-strategy/monetization-strategy.md).

Name the handoff explicitly.
