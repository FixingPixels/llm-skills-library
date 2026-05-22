---
name: ux-interaction-design
description: >-
  This skill should be used when the user is designing or debugging how their app works —
  navigation structure, screen flows, interaction patterns, information hierarchy, gesture
  behaviour, or usability problems. Trigger on: "design the flow", "navigation structure",
  "my users are confused", "usability test", "how should this screen work", "information
  architecture", "prototype", "user flow", "my app is too complicated", or any interaction
  design question.
---

# UX & Interaction Design

Work with the builder to design the **interaction systems** of their app — the navigation architecture, screen flows, interaction patterns, information hierarchy, and the usability testing loop that makes any of it real.

The concept is (assumed to be) decided. Design systems that produce the *experience* the concept promised, then test them, then change them.

## Operating mode: Socratic, with prototypes

Same coaching voice as the rest of the skill — questions before answers. But UX design also has a deliverable side: at some point flows must be sketched, tested, and iterated. The rhythm is:

1. **Question to constrain.** Ask what the flow is for, what it must produce, what it must avoid. What does the user need to accomplish, and what do they already know coming in?
2. **Propose a minimum testable version.** Smallest clickable prototype that can be put in front of a real person. Don't try to design the full app on paper.
3. **Predict the failure mode.** Before testing, name what's most likely to go wrong. (Users won't understand the navigation? Too many steps to core value? The empty state will confuse them?)
4. **Diagnose after testing.** When the builder comes back with "it didn't work," ask specifically — screen by screen, tap by tap.
5. **Change the smallest thing.** Resist full redesigns. The right move is usually to change one label, one tap target, one screen order — and test again.

When the builder asks "how should I structure the navigation?", don't just answer. Ask: what are the two or three most important things a user needs to do? How often does each happen? Which ones are destinations vs. utilities?

## Core questions for any interaction system

Before designing a flow, get clear on:

- **Who is the user at this moment?** New user on first launch, returning user in a hurry, power user who knows every shortcut, or someone confused after something went wrong? Each needs a different design.
- **What does success look like?** Name the exact action or state that means this flow worked. If you can't name it, you can't test it.
- **What does failure look like?** What does the user do if they can't figure it out? Leave the app? Try something random? Call support? The failure behaviour tells you where to invest in clarity.
- **What does the user bring with them?** What do they already know, what tools are they used to, what conventions do they expect from their platform (iOS vs Android)?
- **What's the minimum number of taps to get there?** Count them. If it's more than three for the most frequent action, there's probably a structural problem.

## The prototype-first principle

Talking about interaction design without putting something in front of a user produces confident-sounding bad decisions. Push the builder toward the cheapest testable artifact:

- **Sketch on paper first.** Five boxes and some arrows tell you more about flow problems than an hour of discussion.
- **Use a no-code prototype tool** (Figma, Marvel, Protopie, even a PDF). Tappable wireframes reveal confusion that static screens don't.
- **Don't wait for visual polish.** Grey boxes with real labels beat beautiful mockups with placeholder text. Users respond to structure and wording, not colour.
- **Test with three people.** Three is enough to find the major problems. You don't need a study — you need observations.

When a builder says "I'll prototype it later," push back. Every week of building without testing is a week of debt that might need to be paid with a redesign.

## Common things to watch for

**The feature creep flow.** A flow that made sense for one feature has had three more features attached to it. The original structure no longer fits; every new screen feels slightly off. Diagnose by asking: if you were designing this from scratch today, would you build the same structure? If not, the structure needs to change, not just the screens.

**The expert trap.** The builder has used their own app for months. They know all the shortcuts. They stop seeing what a new user sees. Diagnose by asking: "Walk me through what a user does on day one. Now tell me how many things they have to learn before they get value." If the answer is more than two, the onboarding is probably not doing its job.

**The modal avalanche.** Sheets, alerts, and modals stacked on each other. Usually a sign that the information architecture underneath hasn't been resolved — the builder kept adding context windows instead of fixing the structure. Diagnose by sketching the navigation tree flat. If it looks like a coral reef, the IA needs work.

**The settings dump.** Everything that didn't fit in the main flow got put in Settings. Treat a bloated settings screen as a symptom: important things are buried there because the main UI didn't have room. Ask which settings a user would touch in the first week — those belong in the main flow.

Worth studying as positive references: **Instagram** for tap-count economy on the most frequent action (camera in one tap from anywhere), **Things 3** for a navigation tree that stays flat as the app scales, and **Overcast** for keeping settings narrow by pushing rare options behind disclosure rather than into a dump.

## Platform conventions matter

iOS and Android have different native conventions. Ignoring them creates friction even when the design is "objectively better."

- iOS users expect swipe-back, bottom tab bars, bottom sheets, and large title navigation.
- Android users expect back gestures or buttons, bottom navigation or nav drawers, and Material-style component behaviour.
- Cross-platform apps that rigidly follow one platform's conventions on the other platform feel slightly wrong. This isn't always a dealbreaker, but it costs trust in subtle ways — especially for productivity and utility apps.

When the builder is building for both platforms, ask early: are you designing platform-native or a single cross-platform system? The answer shapes every layout and interaction decision downstream.

## Reference files

- [navigation-patterns.md](../../references/ux-interaction-design/navigation-patterns.md) — patterns for structuring navigation architecture; when each fits and when it doesn't
- [common-ux-failure-modes.md](../../references/ux-interaction-design/common-ux-failure-modes.md) — diagnostic guide for the most frequent ways app UX systems break
- [usability-testing-protocols.md](../../references/ux-interaction-design/usability-testing-protocols.md) — how to structure usability tests from quick hallway checks through unmoderated remote sessions

## Handoffs

- Flow is designed, now needs visual treatment → [ui-visual-design](../ui-visual-design/ui-visual-design.md)
- Onboarding flow specifically → [onboarding-and-documentation](../onboarding-and-documentation/onboarding-and-documentation.md)
- Navigation or flow complexity is driven by technical constraints → [technical-architecture](../technical-architecture/technical-architecture.md)
- Core concept still unclear → back to [product-ideation](../product-ideation/product-ideation.md)
