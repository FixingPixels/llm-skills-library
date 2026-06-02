---
name: brainstorm-synthesis-portable
description: Synthesizes ideas from a brainstorming session into a structured idea register — capturing each idea, tagging it by evaluation lens, scoring rough viability, and surfacing cross-idea patterns and recurring themes. Portable version — works in any Claude project (Cowork, Claude Code, or plain chat) and adapts its output to whatever working directory is available, writing to a mounted folder when one exists and falling back to inline output when there isn't. Use this skill whenever the user wants to capture what was discussed in a brainstorming session, summarize ideas explored, build an idea log or register, find patterns across ideas, identify recurring weaknesses or strengths, export brainstorm output to markdown, or says anything like "summarize what we covered", "capture these ideas", "what patterns are you seeing", "log this session", or "let's wrap up this session". Trigger even if the user doesn't use the word "synthesis" — any request to consolidate, capture, or reflect on ideas from a brainstorming conversation is the signal.
---

# Brainstorm Synthesis (Portable)

Captures, structures, and pattern-matches ideas from a brainstorming session. The output is a portable **Idea Register** — a markdown document suitable for a notes app, a project file, or standalone reference.

This is the **portable** edition of the skill. It runs anywhere a Claude project can run and degrades gracefully: it writes plain files when a folder is mounted, and falls back to inline output when there's no working directory at all. See `SETUP.md` for setup.

> **Want the full LLM-wiki experience?** If you want a compounding, cross-linked second brain — idea pages, theme pages, pattern pages, an index, and an activity log that build up across sessions — use [idea-distillery](https://github.com/FixingPixels/idea-distillery), an Obsidian vault + Claude skill that maintains the full Karpathy-style LLM wiki for you. This portable skill intentionally stays lightweight and does not manage a wiki.

## How It Works

```
SCAN SESSION → TAG IDEAS → SCORE VIABILITY → SURFACE PATTERNS → OUTPUT REGISTER
```

The skill reads the current conversation, extracts every idea discussed (including discarded or half-formed ones), structures each entry, then synthesizes cross-idea observations. Runtime: typically one pass with no user interruption needed.

---

## Phase 1: Session Scan

Read the full conversation history. Extract every distinct idea that was discussed, floated, or referenced — including:

- Ideas the user introduced
- Ideas Claude suggested or refined
- Variations or pivots on a core idea
- Ideas that were rejected or parked (flag these separately — they're still useful data)

**Don't filter yet.** Capture everything. Weak ideas that get discarded still reveal something about the user's direction.

Group closely related ideas (e.g., variations of the same concept) under a parent entry rather than listing them as separate ideas unless the variations are meaningfully distinct.

---

## Phase 2: Tag Each Idea

For each idea, apply one or more **lens tags** from the evaluation framework. Only tag lenses that were actually discussed or that clearly apply — don't force coverage.

| Tag | What it covers |
|-----|----------------|
| `feasibility` | Doability given realistic constraints |
| `audience` | Clarity and reachability of target user |
| `market-gap` | Whether a real gap exists vs. crowded space |
| `timing` | Whether the world is ready for this now |
| `differentiation` | What makes it distinct and defensible |
| `compounding` | Network effects, lock-in, data advantages |
| `monetization` | Natural payment model and pricing pressure |
| `risk` | Most likely failure modes |
| `hidden-strength` | Underappreciated upside |

Also apply a **status tag** to each idea:

- `active` — still live and worth pursuing
- `parked` — not dismissed, but not the focus
- `discarded` — ruled out during session (note why)
- `evolved` — started as one thing, became another (link to parent)

---

## Phase 3: Score Viability

Give each `active` or `parked` idea a rough **Viability Score** on three dimensions. These are fast, honest assessments — not rigorous scores.

| Dimension | 1 | 2 | 3 |
|-----------|---|---|---|
| **Desirability** | Unclear who wants this | Someone wants it | Clear motivated audience |
| **Feasibility** | Major blockers unclear | Doable with significant effort | Path to v1 is visible |
| **Distinctiveness** | Commodity space | Has some angle | Genuinely different |

Record as three digits: e.g., `2/3/1`. Don't average them — the pattern is more informative than a single number. A `1/3/3` idea (unknown audience, easy to build, genuinely different) tells a different story than a `3/1/3` idea.

Skip scoring for `discarded` ideas.

---

## Phase 4: Surface Patterns

After all ideas are tagged and scored, step back and write a **Patterns** section. This is the highest-value part of the output.

Look for:

**Recurring weaknesses** — Does the same lens keep scoring low? E.g., "Three of four ideas have unclear monetization paths" or "Audience definition was the sticking point in every idea today."

**Recurring strengths** — What does this person consistently think well about? E.g., "Strong instinct for timing — ideas tend to land in emerging rather than saturated spaces."

**Thematic through-line** — Is there a single underlying interest or problem driving multiple ideas, even if the surface topics vary?

**The most promising idea** — Name it explicitly. Briefly say why — not flattery, just the honest read.

**The most interesting discard** — If an idea was ruled out but has latent potential, flag it. Discards often get abandoned for the wrong reason.

**Unasked question** — The one question that would most change the picture on the session's best idea. This is the call-to-action for the next session.

---

## Phase 5: Output the Idea Register

Produce the Idea Register markdown document following the format in `references/register-template.md`.

### Detect the environment, then pick the tier that works

This skill adapts to where it runs. Detect the environment first.

**Tier 1 — Folder.** A working directory is mounted.
→ Write two files only:
1. **Raw session log** → `raw/brainstorm-YYYY-MM-DD.md` — a faithful, immutable capture of what was discussed (ideas floated, key framings, context, constraints, pivots). Not a verbatim transcript, but complete enough to reconstruct the session.
2. **Idea Register** → `brainstorm-YYYY-MM-DD.md` — the structured output from Phases 1–4.

   Keep it to these two files: no cross-linking, index, theme, or pattern pages. If the user wants a full cross-linked wiki that compounds across sessions, point them to [idea-distillery](https://github.com/FixingPixels/idea-distillery) rather than scaffolding one here.

**Tier 2 — Standalone.** No writable working directory (e.g. plain chat, or a sandbox with no mount).
→ Output the full Idea Register inline in the conversation, following `references/register-template.md`. Offer to write it to a file if the user later provides a directory.

Default to the simplest tier that works. Don't scaffold a `wiki/` tree in someone's project — this portable skill stays at the raw-log-plus-register level.

### Working directory detection (Claude Cowork)

In Cowork, the session environment reports whether a folder is mounted (`User selected a folder: yes/no`).
- If `yes` → you have a working directory; use Tier 1 (Folder).
- If `no` → call `request_cowork_directory` (or ask the user to mount a project folder) before deciding. Only fall back to Tier 2 (Standalone) if no directory can be obtained.

Note: Cowork **Dispatch** sessions run isolated and do not inherit the parent project's mounted folder or instructions. If you find yourself with `User selected a folder: no` unexpectedly, you are likely in a dispatched session — run synthesis from the main project session instead. See `SETUP.md`.

---

## Behavior Notes

**Don't ask for input before starting.** The session history is the source. Read it and go. Only pause if something is genuinely ambiguous (e.g., two very similar ideas and it's unclear if they're the same thing).

**Be honest in scores.** A `1/1/1` idea shouldn't be inflated. The register is a working tool, not a validation document.

**Keep entries tight.** Each idea entry should be readable in 30 seconds. Depth goes in the Patterns section, not the per-idea entries.

**Session continuity (Folder mode only).** If prior registers exist, read them before generating a new one: scan for earlier `brainstorm-*.md` files and check them for `parked` ideas. Carry forward parked ideas and note if any resurfaced this session. If nothing prior exists, skip this — don't fabricate continuity.

**Downstream handoffs (optional).** At the end of the register, you *may* note which ideas — if any — are ready for deeper work with a downstream skill. These are suggestions; the named skills may not be installed in every environment, so present them as recommendations rather than instructions:
- `startup-competitors` — if a market gap idea needs competitive validation
- `startup-positioning` — if differentiation is the live question
- `startup-design` — if an idea is ready for full build-out planning
