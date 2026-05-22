# Problem/Solution Fit

Use this when a builder has a solution without a clear problem, a problem without a clear solution, or a pairing that feels arbitrary or forced.

## The integration test

A problem and a solution are well-paired when **changing one breaks the other.** If you could re-frame the problem to something else without changing your solution at all, the pairing is shallow. If you could swap the solution for any other common app pattern and still solve the problem equally well, the pairing is shallow.

Examples of tight pairings:

- **Duolingo** — gamified streaks and short lessons because language learning dies from inconsistency and discouragement, not lack of content. The streak mechanic only makes sense because the problem is *retention*, not *instruction*. A traditional course structure wouldn't solve the same problem.
- **Calm / Headspace** — guided audio with ambient sound because the problem is an anxious, distracted mind that won't sit still for text. The solution (voice + sound) is the only format that works; a written meditation guide solves a different problem.
- **Notion** — infinitely flexible structure because the problem is that different people and teams think in fundamentally different shapes. A rigid template structure (like most productivity tools) would fail the same users.
- **Superhuman** — keyboard-first speed because the problem is email *volume and latency*, not email *organisation*. Mouse-based design couldn't solve the same thing.

Examples of weak pairings (solution looking for a problem):

- A journaling app that adds AI summaries of your entries. The user's problem with journaling is usually *friction to start* or *forgetting to do it* — not *forgetting what they wrote*. The AI feature solves something else.
- A habit tracker that gamifies with badges and levels. The user's problem with habit formation is usually the habit being hard, not the tracking being unfun. Gamification is wallpaper over a design problem.

## Pairing prompts

When a builder brings a problem:

- What does the solution need to do that *only works* because of this specific problem? If the solution is general-purpose, the fit may be weak.
- What is the *format* the problem demands? Audio? Real-time? Offline? Asynchronous? The right format is often non-obvious and strongly constrained by the problem.
- What would make the solution *not work* for a different problem? Name that. It's the shape of the fit.
- What does the problem make *scarce* for the user? Time, attention, money, confidence, information? Scarcity drives solution design — an app that ignores the scarcity won't solve the problem.

When a builder brings a solution:

- What human experience does this solution *feel like*? A scheduling tool feels like negotiation. A photo editor feels like making something look how you imagined it. A tracker feels like accountability. What does yours feel like — and what problem produces that feeling?
- Who is in pain right now and doesn't have a version of this? That's the user. Start there.
- What does the solution *require of the user*? (Time to set up, data to input, habit to form, permission to grant.) Whatever it requires is a friction cost. Is the problem painful enough to pay that cost?

## The "why now" test

Every successful product either solves a problem that's new, or solves an old problem in a way that's newly possible. Ask:

- What has *changed* — in technology, behaviour, culture, or the market — that makes this solvable now when it wasn't two years ago?
- If this idea is obvious, why hasn't it shipped already? (Honest answers: it's technically hard, the audience was too small, the behaviour shift just happened, someone tried and failed. Find out which.)
- If the answer is "nothing has changed, this has always been a problem," push harder: either someone has already built it, or there's a reason it hasn't been built. Both deserve investigation before proceeding.

Strong "why now" examples:
- *Shortform / Blinkist* — grew alongside the shift to audio commutes and podcast culture. The problem (not enough time to read) wasn't new; the listening-while-doing behaviour was.
- *Locket widget* — possible only after iOS 14 added widget support. The problem (staying connected with close friends) was old; the home-screen access was new.
- *Perplexity* — possible only after large language models reached the quality bar where AI-written prose was trustworthy enough to replace link-clicking.

## The switching cost test

If users already have a solution — even a bad one — your product has to be significantly better to earn a switch. Ask:

- What does the user currently use? How entrenched is it? (A spreadsheet that took three hours to build is harder to replace than a free app they found last Tuesday.)
- What does the user have to *give up* to switch? Their data history, their habits, the fact that their team already uses something else?
- How much better does your solution need to be to justify the switch? The answer is almost always "more than you think."

This is the most underestimated test in early ideation. Many products solve a real problem but fail because the switching cost exceeds the value delta — especially in markets where an incumbent has captured behaviour even with a mediocre product.

## Signs the pairing is working

- The builder can describe a single **user moment** that only makes sense with this problem and this solution together. Remove either and the moment dissolves.
- A target user (not the builder's friends, but a real representative user) says "I've wanted this" — not "that's interesting" or "I'd probably use that."
- The format demanded by the problem and the format of the solution are the same. You're not making a voice app because voice is trendy; you're making a voice app because the problem happens with your hands full.
- The builder can explain why the *second-best solution* doesn't work. This is the clearest signal of genuine fit.
