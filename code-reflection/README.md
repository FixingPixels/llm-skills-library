# code-reflection

A framework of Claude [Agent Skills](https://docs.anthropic.com/en/docs/agents-and-tools/agent-skills)
that read your codebase and tell you who you are as a builder — then give you a
prioritized plan to grow.

---

## Philosophy

Growth tools for developers tend to do one of two things: tell you what
technologies to learn (always more, always newer) or optimize your profile for
job applications (keywords, ATS scores). Neither helps you understand how you
actually think or build.

`code-reflection` starts from a different premise: your existing work already
contains everything needed to understand your strengths and your edges. The
codebase is the evidence. The analysis is just careful reading.

---

## What it does

Most developer tools look forward: autocomplete, linting, code review.
`code-reflection` looks inward. It ships two skills:

- **`repo-capability-analyst`** — point it at any codebase and it produces two
  files:
  - **`PROFILE-REPORT.md`** — a capability profile extracted from your code and
    commit history. Hard skills (languages, frameworks, architecture, AI/LLM
    integration) and soft skills inferred from behavioral evidence
    (documentation quality, system thinking, complexity calibration,
    communication craft). Every claim is sourced to a specific file or commit
    pattern.
  - **`GROWTH-PLAN.md`** — an epic-style growth plan addressing the gaps. Each
    epic explains why the gap matters *in this specific codebase*, not generic
    advice, and breaks it into file-level tasks.
- **`growth-planner`** — reads your existing `GROWTH-PLAN.md`, finds the
  highest-priority open epic, asks about your current constraints, and produces
  a focused, achievable plan for this work session.

---

## Why codebases

Your code is behavioral evidence. It doesn't lie, perform, or optimize for an
audience the way a resume or LinkedIn profile does. The architecture choices you
make, the error messages you write, the things you choose *not* to build — these
are direct signals of how you actually think.

So is your commit history. How you describe changes, whether you work in focused
increments or large blobs, whether you acknowledge the limits of your own work
in commit messages — signals that static file reading can't surface. When git
history is available, `code-reflection` uses it to confirm, deepen, or sometimes
contradict what the files suggest.

---

## Installation

These are portable Agent Skills. Install each skill folder wherever Claude looks
for skills:

| Scope | Location |
|-------|----------|
| Personal (all your projects) | `~/.claude/skills/<skill-name>/` |
| Project (shared via the repo) | `.claude/skills/<skill-name>/` |
| Claude.ai | Upload the skill folder in **Settings → Capabilities → Skills** |

For example, to install both skills for a single project:

```bash
mkdir -p .claude/skills
cp -r code-reflection/skills/repo-capability-analyst .claude/skills/
cp -r code-reflection/skills/growth-planner .claude/skills/
```

No required setup. A shell (for `git log`) is optional — without it, the
analysis uses file evidence only, with no penalty.

---

## Usage

Skills are invoked by description — just ask in plain language.

**Analyze:** "Analyze this repo and tell me who I am as a builder." The
`repo-capability-analyst` skill prioritizes high-signal files (Tier 1 first,
capped at 30 files), extracts capability signals, and writes `PROFILE-REPORT.md`
and `GROWTH-PLAN.md` to your repo root. On a fresh repo it starts clean; on
later runs it preserves completed tasks and only surfaces gaps still open.

**Make progress:** "What should I work on next?" The `growth-planner` skill
finds the top open epic, asks one question about your constraints, and gives you
a focused plan for the session — then offers to start immediately.

---

## How it's structured

```
code-reflection/
├── CONVENTIONS.md                 # shared authoring conventions
└── skills/
    ├── repo-capability-analyst/
    │   ├── SKILL.md               # lean orchestrator
    │   ├── references/            # sampling, signals, output rules (read on demand)
    │   └── templates/             # PROFILE-REPORT / GROWTH-PLAN skeletons
    └── growth-planner/
        └── SKILL.md
```

The analyst skill uses **progressive disclosure**: `SKILL.md` holds only the
workflow and pointers, while detailed guides and the large output templates live
in `references/` and `templates/` and are read only at the step that needs them.
This keeps the always-loaded context small. See `CONVENTIONS.md` for the rules a
new skill should follow.

---

## Smart sampling

`code-reflection` doesn't read every file — it reads the right files.

- **Git history (if a shell is available):** before touching files, it reads the
  last 50 commits — message quality, atomicity, iteration patterns, and honest
  self-assessment ("hacky", "temp", "not ideal" are signals). Skipped silently
  if no shell or not a git repo. No penalty.
- **Tier 1 (always):** README, dependency manifests, CI/CD configs,
  infrastructure, root configs, context files (`CLAUDE.md`, `AGENTS.md`).
- **Tier 2 (sampled):** entry points, one file per top-level directory, any file
  with `prompt`, `agent`, `llm`, `context`, or `tool` in its name.
- **Tier 3 (skipped):** test files, generated output, lock files.

Cap: 30 files per run.

---

## Soft skills from code and commits

Code is behavioral evidence. `code-reflection` looks for documentation quality,
system thinking, complexity calibration, communication craft, context
engineering, epistemic character, tooling investment, and (from git history)
ownership & iteration. These aren't self-reported — they're inferred from how
you actually build. In a world where AI handles more of the execution layer,
these are the skills that compound.

---

## Updating your profile

Re-run the `repo-capability-analyst` skill any time. It checks for existing
reports, preserves completed epic tasks, and only generates new epics for gaps
still open — your progress is never lost. A cadence that works well: re-run
after finishing a significant feature or epic, not on every commit. Works best
on repos with 10+ files and some git history.

---

## Output files and privacy

`PROFILE-REPORT.md` and `GROWTH-PLAN.md` are written to your repo root. Add them
to `.gitignore` to keep them private, or commit them as portfolio signal.

---

## Roadmap

- [ ] `content-capability-analyst` skill — extends profiling to articles,
  Obsidian vaults, and custom GPT definitions
- [ ] `multi-repo-analyst` — synthesize a profile across several codebases
- [ ] Cognitive fingerprint dimension — reasoning style, epistemic stance, and
  temporal orientation inferred from code patterns

New skills follow the structure in `CONVENTIONS.md`.

---

## License

MIT
