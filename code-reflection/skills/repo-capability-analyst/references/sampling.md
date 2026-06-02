# Evidence Gathering — Git History + File Sampling

This guide covers Step 2: collecting the evidence the rest of the analysis
draws on. Do the git pass first (it is cheap and high-signal), then sample
files.

## Git history (if a shell is available)

Before reading any files, check whether you can run shell commands (e.g. the
Bash tool in Claude Code). If you can, and the project is a git repo, gather
the last 50 commits:

```bash
git log -n 50 --pretty=format:'%h%x09%an%x09%ad%x09%s' --date=short
git log -n 50 --stat --pretty=format:'%h %s'
```

Extract these signals from the output:

- **Commit message quality** — descriptive and contextual vs. terse ("fix bug")
  vs. absent context. Note the general pattern, not outliers in either direction.
- **Commit atomicity** — small focused commits vs. large mixed commits. A
  pattern of "fixed everything" or "WIP" blobs is a signal.
- **Iteration patterns** — does the developer revisit and refine files over
  time, or is most work single-pass? Frequent follow-up commits to the same
  files suggest active ownership.
- **Honest self-assessment** — "hacky", "temp", "TODO: clean this up", "not
  ideal but..." in commit messages are evidence of epistemic character: the
  developer knows the limits of their own work.
- **Velocity and consistency** — commit frequency over time. Bursts followed by
  silence vs. a steady consistent rhythm.
- **Branch and merge patterns** — if visible, feature branches with descriptive
  names vs. committing directly to main.

If no shell is available, or the project is not a git repo, note this once in
the output and proceed with file analysis only. **Do not treat the absence of
git history as a gap** — it is a tooling constraint, not a skill signal.

## Smart sampling

Do NOT attempt to read every file. Cap at **30 files total**. If a codebase
search/semantic tool is available, use it to locate Tier 2 files efficiently.
Follow this priority order.

### Tier 1 — Always read

- `README.md`, `README.rst`, top-level docs
- Dependency manifests: `package.json`, `pyproject.toml`, `Cargo.toml`,
  `go.mod`, `requirements.txt`, `pom.xml`, `build.gradle`
- CI/CD: `.github/workflows/*.yml`, `Makefile`, `justfile`
- Infrastructure: `Dockerfile`, `docker-compose.yml`, `*.tf`, files under
  `infra/`, `deploy/`, `k8s/`
- Root configs: `tsconfig.json`, `vite.config.*`, `next.config.*`, `.eslintrc*`,
  `jest.config.*`, `prettier.config.*`
- Context/agent files: `CLAUDE.md`, `AGENTS.md`, `CONTEXT.md`, `.cursorrules`,
  `.cursor/rules/*.mdc`, `ARCHITECTURE.md`

### Tier 2 — Sample strategically

- Entry points: `main.*`, `index.*`, `app.*`, `server.*`, `cli.*`
- One representative file per top-level directory
- Any file with `prompt`, `agent`, `llm`, `context`, `chain`, `tool`, or
  `memory` in its name — high signal for AI/context engineering work

### Tier 3 — Skip unless the repo has fewer than 20 files

- Test files: `*.test.*`, `*.spec.*`, `__tests__/`
- Generated output: `dist/`, `build/`, `.next/`, `node_modules/`, `.venv/`
- Lock files (read manifests instead)

### Thin evidence

If fewer than 5 meaningful files are found (excluding manifests, lock files,
and generated output), treat evidence as limited:

- Produce an abbreviated `PROFILE-REPORT.md` with the skills matrix and a short
  capability narrative.
- Keep `GROWTH-PLAN.md` to one epic maximum.
- Explicitly state that the repository is too small for high-confidence profiling.

If the 30-file cap forces skipping directories, note which ones were skipped.
