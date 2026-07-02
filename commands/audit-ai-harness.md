# Audit AI-First Harness

Audit this repository's AI-first development setup and write the findings to `docs/ai-harness.md`. The report is for the repo owner's self-knowledge: what harness exists here, how mature it is, and where it's thin. Evidence over inference — cite file paths for every claim. Read-only except for the report itself.

## 1. Inventory

Search the repo for each of the following. Record what exists, what's absent, and anything malformed or stale.

**Agent context & rules**
- `.cursor/rules/*.mdc` — for each: description, globs, `alwaysApply`, and one line on what it governs
- `.cursorrules` (legacy — flag for migration if present)
- `AGENTS.md`, `CLAUDE.md`, nested variants in subdirectories

**Reusable prompts & skills**
- `.cursor/commands/` — list each command and its purpose
- `.cursor/skills/` (or `SKILL.md` files anywhere) — name, description, whether it bundles scripts/references

**Tooling & integrations**
- `.cursor/mcp.json` — servers configured and what capabilities they add
- Hooks configuration, if any

**Guardrails the agent must satisfy**
- Test setup (framework, coverage config, whether rules/docs tell the agent to run tests)
- Linters/formatters/type checks and how they're enforced (pre-commit, CI)
- CI workflows — note any AI-involved steps (review bots, agent-triggered jobs)

**Context hygiene**
- `.cursorignore`, `.cursorindexingignore`
- Prompt/eval assets: `prompts/`, `evals/`, fixture data for agent testing

**Usage evidence**
- Check git history: are rules/commands recently touched or fossilized? Do commit messages suggest agent-driven work? Distinguish *configured* from *actually used*.

## 2. Synthesize methodology

From the inventory, infer working patterns — each with cited evidence, none asserted without it:
- Development style the harness encodes (spec-first, plan-then-execute, TDD, YOLO)
- What the owner delegates to the agent vs reserves for themselves
- How context is engineered: layered rules vs monolith, scoped vs always-on, docs-as-context
- Recurring conventions that look intentional (naming, structure, review gates)

## 3. Write the report

Write `docs/ai-harness.md` (create `docs/` if needed):

```markdown
---
audited: YYYY-MM-DD
repo: <name>
maturity: minimal | developing | mature
---

# AI Harness Audit

## Summary
<3–5 sentences: what the harness is, its maturity, the single biggest gap>

## Rules & Context
<table: file | scope (always/globs/manual) | governs>

## Commands & Skills
<what exists, what each is for, evidence of use>

## Tooling & MCP
<servers, hooks, integrations>

## Guardrails
<tests, lint, CI gates the agent is held to — and whether rules actually reference them>

## Methodology Observations
<inferred patterns, each with file-path evidence>

## Gaps & Recommendations
<prioritized; max 5; each one actionable>

## Changelog
- YYYY-MM-DD: <what changed since last audit>
```

## Rules

- If `docs/ai-harness.md` already exists, update it in place and append a changelog entry summarizing the delta — don't regenerate from scratch and lose history.
- Keep the report under ~150 lines. Precision beats coverage.
- Mark uncertain inferences explicitly ("possibly", "no evidence of use").
- Never modify rules, commands, configs, or code. Report only.
