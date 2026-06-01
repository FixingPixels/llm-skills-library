---
title: Writing Session
load_at: mode-b
summary: Read voice-profile.md, draft with the self-review checklist, capture feedback in-session, deliver a Post-Session Feedback Summary, and offer an in-place profile update
---

# Writing Session (Mode B)

Mode B turns the living profile into actual drafts and uses each session as a free signal source. The loop has three phases: pre-draft setup, drafting and iteration, and a post-session feedback summary with an offer to update the profile in place.

## Contents

1. [Phase 1 — Pre-draft setup](#phase-1--pre-draft-setup)
2. [Phase 2 — Draft and iterate](#phase-2--draft-and-iterate)
3. [Phase 3 — Post-Session Feedback Summary](#phase-3--post-session-feedback-summary)
4. [Mid-session profile updates](#mid-session-profile-updates)
5. [Targeted edit playbook](#targeted-edit-playbook)
6. [When to refuse Mode B](#when-to-refuse-mode-b)

---

## Phase 1 — Pre-draft setup

1. **Read the profile.** Open `references/voice-profile.md`. If the file does not exist, stop Mode B and run Mode A first (tell the user). If it exists, load the whole file — metadata header, body, and the most recent changelog entry — into context for this session.
2. **Surface low-confidence flags.** If any dimension relevant to the requested content type is flagged low confidence in the metadata header, briefly tell the user up front so they know which parts of the draft to scrutinize.
3. **Clarify only if needed.** Ask up to one or two short questions if the brief is genuinely ambiguous (content type, core message, audience, length, CTA). Don't over-ask.
4. **Start a session journal.** For the rest of the session, keep an internal running list of: (a) corrections the user makes, (b) words/phrases they reject, (c) words/phrases they add or favor, (d) structural changes (opening swaps, paragraph splits, closing rewrites), (e) any explicit "no, I'd never say it like that" / "yes, that's exactly how I'd put it" signals. This journal feeds Phase 3.

---

## Phase 2 — Draft and iterate

1. **Draft using the profile.** Apply Voice Signature, Sentence Structure & Rhythm, Vocabulary (reach-for and avoid lists), Openings/Closings, and Rhetorical Moves verbatim from the profile.
2. **Run the in-profile self-review checklist** before presenting the first draft. If anything fails, fix it before showing the user.
3. **Present the draft** with a single brief framing note (e.g. "Went with a contrast opening — let me know if you'd prefer a question-led version"). Offer alternatives only on request.
4. **Iterate.** Take the user's edits, rewrites, and direction. Every iteration adds entries to the session journal (Phase 1, step 4). Never argue with the user's preferences — they are the ground truth for their own voice.

The user may end the session at any point by accepting a draft, shipping it, or saying they're done. That ends Phase 2 and starts Phase 3.

---

## Phase 3 — Post-Session Feedback Summary

Always run this after every Mode B session, even short ones — including sessions where the user accepted the first draft (in which case the summary is short and the answer to the update offer is usually "no, nothing changed").

Present a structured summary, then ask whether to update the profile. Suggested shape:

```markdown
**Post-Session Feedback Summary**

What we wrote: [content type, one-line topic]
Drafts: [N]

**Feedback I heard:**
- [Bullet per piece of feedback. Use the user's own words where possible. e.g. "Cut 'in essence' — flagged as AI-sounding."]
- [...]

**Editing choices made:**
- [Structural/stylistic moves the user made or directed. e.g. "Replaced the question opener with a flat declarative."]
- [...]

**What this implies about your voice:**
- [Map each notable signal to a profile dimension. e.g. "Lexical Fingerprint -> add 'in essence' to Avoid list."]
- [Be conservative. One strong signal beats five weak inferences. If something is just a one-off preference for this piece, say so and don't propose a profile change for it.]

**Want me to update your voice profile with these signals?**
```

Then wait for the user's answer.

- **On "yes"** (or any clear affirmative): apply targeted edits to `references/voice-profile.md` per the [Targeted edit playbook](#targeted-edit-playbook), append a changelog entry tagged "In-session update" (see [`profile-format.md`](profile-format.md) §4), and confirm what changed.
- **On "no"** (or "not this time"): do nothing. The profile is unchanged. Tell the user the session is closed — and that they can re-open it later by saying "actually, update my profile with what we just did."
- **On "yes but only the X part"**: apply only those signals and explicitly skip the rest in the changelog.

---

## Mid-session profile updates

If the user says, at any point during Phase 2, something like *"add this to my voice profile"*, *"update my profile with that"*, or *"that's actually how I want it from now on"*, apply the update immediately:

1. Apply the targeted edits per the playbook below.
2. Append a changelog entry.
3. Reload the relevant section into context so the rest of the session benefits from the new rule.
4. Continue the writing session.

Do not wait until Phase 3 to capture a signal the user has explicitly asked you to remember.

---

## Targeted edit playbook

A profile update from a writing session should be **surgical**, not a rewrite. Match each signal to the smallest change that captures it.

| Signal from session | Profile change |
|---|---|
| User crossed out a word/phrase and wouldn't accept variants | Add to **Vocabulary -> Avoid these** |
| User reached for the same word/phrase across multiple edits | Add to **Vocabulary -> Reach for these** |
| User rewrote the opener in a recognizable pattern | Add an example to **Openings** and update the dominant-pattern description if the pattern is new |
| User rewrote the closer | Add to **Closings** the same way |
| User shortened or lengthened sentences consistently | Tighten the description in **Sentence Structure & Rhythm** |
| User flagged a structural move as "not me" | Add it to **What This Voice Is NOT** |
| User wrote a passage they explicitly loved | Add it as a new **Signature Example** with a label |
| Format-specific rule for one content type (e.g. "no CTAs on LinkedIn") | Add under that subsection of **Content Type Notes** |
| One-off preference for this piece only | Do nothing to the profile. Note in the changelog as "Considered and skipped — one-off." |

After applying edits, verify the profile still passes the quality gate in [`profile-format.md`](profile-format.md) §5 (no placeholders, every trait still traces to a verbatim source quote, header is internally consistent).

---

## When to refuse Mode B

- The profile does not exist yet. Switch to Mode A.
- The requested content type is wildly outside what the profile covers (e.g. profile is all LinkedIn posts; request is a 10,000-word screenplay). Tell the user the profile may not transfer cleanly and offer to either proceed with caveats or build out more material via Mode A first.
- The user asks for content the voice is documented as never producing (e.g. profile says "never uses bullet lists" and the request is "make this a bullet list"). Surface the conflict and let the user choose to override.
