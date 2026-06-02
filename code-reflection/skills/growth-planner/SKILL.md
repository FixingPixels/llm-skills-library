---
name: growth-planner
description: >-
  Turns an existing GROWTH-PLAN.md into a focused, achievable plan for the
  current work session. Finds the highest-priority open epic, asks about current
  constraints, and produces file-level next steps. Use when the user asks what
  to work on next, wants to make progress on their growth plan, or asks to work
  on a growth gap. Requires a GROWTH-PLAN.md (produced by repo-capability-analyst).
---

# Growth Planner

Helps the user make real progress on the growth plan produced by the
`repo-capability-analyst` skill, one session at a time.

## Step 1 — Check for GROWTH-PLAN.md

Look for `GROWTH-PLAN.md` in the repo root.

- **It doesn't exist** → tell the user to run the `repo-capability-analyst`
  skill first to generate their growth plan, then stop.
- **It exists** → read it in full and continue. Also read `PROFILE-REPORT.md`
  if present, to inform suggestions with the user's known strengths.

## Step 2 — Identify the current epic

Find the highest-priority epic that has at least one unchecked task. Tell the
user:

- Which epic you identified and why (priority + effort)
- How many tasks remain
- Any preconditions not yet met

If every epic is fully checked off, congratulate the user and suggest re-running
`repo-capability-analyst` to check whether new gaps have emerged. Then stop.

## Step 3 — Ask one question before proceeding

Ask exactly one question and wait for the answer. Do not suggest tasks first:

> "What are your constraints right now? For example: time available, energy
> level, or any parts of the codebase you want to avoid."

## Step 4 — Build a focused work plan

Using their constraints and the epic's task list, produce a tight plan for this
session:

- Select the subset of tasks achievable within their constraints.
- Order them so each task builds on the previous one.
- For each task, give a concrete first step at the file level — not "add tests"
  but "create `tests/unit/firebase-service.test.js` and write a test for the
  `readSession()` function".
- Flag any task with a hidden dependency or risk worth knowing before starting.

A focused plan for two tasks completed fully beats a sprawling plan for six
tasks started and abandoned.

## Step 5 — Offer to start immediately

After presenting the plan, ask:

> "Want me to start on the first task now?"

If yes, begin implementation directly — don't re-summarize the plan, just start,
referencing the specific files named in the task. If no, leave the plan as a
reference and let the user lead.
