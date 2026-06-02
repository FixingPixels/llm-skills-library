# Output Rules — Field Population, Vocabularies, Quality Bar

This guide governs Steps 5 and 6: how to fill the templates and what bar the
output must clear. Read it alongside `templates/profile-report.md` and
`templates/growth-plan.md`.

## PROFILE-REPORT.md fields

- `> Analyzed:` — file count and commit count, or "no git history".
- `> Last updated:` — today's ISO date.
- **Hard skills table** — omit rows where no evidence was found.
- **Signal Strength** must be one of: `Core`, `Strong`, `Solid`, `Present`,
  `Exploratory`. A bar prefix is allowed, e.g. `████████░░ Strong`.
- **Soft skills table** — every Assessment must use one of: `Exceptional`,
  `Thorough`, `Strong`, `Solid`, `Adequate`, `Sparse`, `Limited signal`. Every
  Evidence cell must cite a file path or "git history".
- Omit the **Ownership & Iteration** row if git history was unavailable.
- **Narrative** — second person, each section a paragraph. Omit the
  `AI & context engineering` section if no AI/LLM evidence was found. The
  `Honest gaps` section is required and must include 2-3 constructive gaps.
- **Sources** — list every file read; note git-history status.

## GROWTH-PLAN.md fields

- `> Based on:` — reference to PROFILE-REPORT.md and today's date.
- `> Last updated:` — today's ISO date.
- **Progress table** — one row per epic, status as "0 / N tasks".
- **Epic headings** — gap name, priority (High/Medium/Low), effort (S/M/L),
  preconditions (None, or Epic N).
- **"Why this matters"** — codebase-specific, names actual files, explains
  second-order consequences. Generic rationale is not acceptable.
- **Tasks** — file-level specific, formatted as `- [ ] task`.

## Update runs (GROWTH-PLAN.md)

When `GROWTH-PLAN.md` already exists:

- Read the existing file before generating new output.
- Identify epics with all tasks checked — do not recreate them.
- For partially complete epics, carry checked tasks forward exactly as the user
  left them.
- Only generate new epic sections for gaps that are still open.
- Update the Progress table to reflect current completion state.

## Quality bar

- Every claim in the skills matrix must cite a source — file path or "git
  history". No unsupported claims.
- The narrative must include at least one non-obvious observation — something
  about *how* they build, not just *what* they've built. If git history is
  available, at least one observation must come from it rather than static file
  analysis.
- Each epic's "Why this matters" must reference specific files or patterns from
  this codebase. Generic rationale is not acceptable.
- Tasks must be file-level specific ("add tests for `firebase-service.js`" not
  "improve test coverage").
- If evidence is thin, say so. Honesty > impressiveness.
- Soft-skill assessments must be grounded in multiple observations. A single
  data point is insufficient — note it as "limited signal".
- If git history was unavailable, do not penalize the analysis — note it once
  and move on. Do not treat missing history as a gap in the developer's skills.
