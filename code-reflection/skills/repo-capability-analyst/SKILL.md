---
name: repo-capability-analyst
description: >-
  Analyzes a codebase to produce a role-agnostic capability profile and a
  prioritized growth plan from file evidence and optional git history. Writes
  PROFILE-REPORT.md and GROWTH-PLAN.md to the repo root. Use when the user asks
  to analyze their repo, infer their skills from code, profile a codebase, or
  generate growth gaps and epics.
---

# Repo Capability Analyst

Reads the current codebase and produces two markdown files in the repo root:

- `PROFILE-REPORT.md` — capability profile (skills matrix + narrative)
- `GROWTH-PLAN.md` — epic-style growth plan (prioritized gaps + tasks)

The codebase is the evidence. Every claim must cite a source — a file path or
"git history". No unsupported claims.

## Workflow

Work through these steps in order. Each references a detailed guide; read the
guide when you reach that step, not before.

```
- [ ] Step 1: Check for existing reports (fresh run vs. update run)
- [ ] Step 2: Gather evidence — git history + tiered file sampling
- [ ] Step 3: Extract signals — hard skills, soft skills
- [ ] Step 4: Synthesize — confirmations, contradictions, the through-line
- [ ] Step 5: Write PROFILE-REPORT.md
- [ ] Step 6: Write GROWTH-PLAN.md
- [ ] Step 7: Confirm to the user
```

### Step 1 — Check for existing reports

Look for `PROFILE-REPORT.md` and `GROWTH-PLAN.md` in the repo root.

- **Neither exists** → fresh run. Continue to Step 2.
- **Either exists** → update run. Read both in full first. Note which epics in
  `GROWTH-PLAN.md` have all tasks checked (closed — do not resurface) and which
  are partially complete (preserve checked tasks exactly). Carry this context
  through the remaining steps.

### Step 2 — Gather evidence

Read `references/sampling.md` and follow it. It covers git-history analysis
(if a shell is available) and the tiered file-sampling strategy with a 30-file
cap.

### Step 3 — Extract signals

Read `references/signals.md` and follow it to extract hard skills and soft
skills, tracking a named source for every finding.

### Step 4 — Synthesize

Still in `references/signals.md`: look for confirmations between git history and
files, contradictions worth naming, recurring patterns, gaps, and the single
through-line that characterizes the developer.

### Step 5 — Write PROFILE-REPORT.md

Read `references/output-format.md` for field rules and the quality bar, then
fill `templates/profile-report.md` and write the result to `PROFILE-REPORT.md`
in the repo root. On an update run, reflect the current codebase — do not carry
forward stale observations.

### Step 6 — Write GROWTH-PLAN.md

Fill `templates/growth-plan.md` and write the result to `GROWTH-PLAN.md` in the
repo root. On a fresh run, generate epics for all gaps, ordered by priority. On
an update run, follow the update rules in `references/output-format.md` to
preserve completed work.

### Step 7 — Confirm

Tell the user:
- Whether this was a fresh run or an update
- How many gaps were identified (fresh) or remain open (update)
- The names of the two files written
- One sentence on the most important gap to address first
- The opening sentence of the Capability Narrative
- The title of the highest-priority epic

## References

- `references/sampling.md` — git history + tiered file sampling
- `references/signals.md` — hard/soft skill dimensions + synthesis
- `references/output-format.md` — field rules, vocabularies, quality bar, update rules
- `templates/profile-report.md` — PROFILE-REPORT.md skeleton
- `templates/growth-plan.md` — GROWTH-PLAN.md skeleton
