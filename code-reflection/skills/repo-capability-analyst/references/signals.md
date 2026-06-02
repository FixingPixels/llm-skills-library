# Signal Extraction + Synthesis

This guide covers Step 3 (extract signals) and Step 4 (synthesize). Track every
finding with a named source — a file path or "git history". No unsupported
claims.

## Hard skills

| Dimension | What to look for |
|---|---|
| **Languages** | All languages present; weight by file count and apparent LOC |
| **Frameworks & Libraries** | Full list from manifests and import statements |
| **AI / LLM Integration** | Anthropic/OpenAI/LangChain SDKs, vector DBs, prompt template files, agent scaffolding, MCP tool definitions, `CLAUDE.md`/`AGENTS.md`, RAG pipelines, tool-use patterns |
| **Infrastructure & DevOps** | CI/CD pipelines, containers, IaC, cloud SDKs, deployment targets |
| **Architecture Patterns** | REST/GraphQL APIs, event-driven, microservices, monolith, CLI tools, serverless, plugin systems |
| **Data & Storage** | DB choices, ORM usage, migrations, caching, data pipeline patterns |
| **Testing & Quality** | Test framework presence, coverage config, type checking, linting, pre-commit hooks |

## Soft skills (inferred from behavioral evidence)

These are behavioral signals — infer from evidence, not assumption. Where git
history is available, use it to confirm, contradict, or deepen what the static
file analysis suggests.

| Dimension | File signals | Git signals (if available) |
|---|---|---|
| **Documentation Quality** | README depth, inline comments, docstrings, architecture docs | Commit messages that explain *why*, not just *what* |
| **Context Engineering** | Structured prompt files, `CLAUDE.md`, tool definitions as first-class artifacts | Commit history showing prompt iteration and refinement |
| **System Thinking** | Extensibility hooks, separation of concerns, config-over-magic, anticipating misuse | Refactoring commits that improve structure without changing behavior |
| **Complexity Calibration** | Architecture proportionate to problem scope; what's NOT built | Absence of speculative commits; focused scope per change |
| **Communication Craft** | Error message quality, naming clarity, writing in READMEs | Commit message clarity and consistency as a communication habit |
| **Epistemic Character** | Defensive handling for uncertain cases, TODOs that acknowledge limits | "Hacky", "temp", "not ideal" in commits — honest self-assessment |
| **Tooling Investment** | Custom scripts, Makefile targets, DX improvements | Commits dedicated to developer experience with no user-facing change |
| **Ownership & Iteration** | Long-lived files with consistent maintenance | Steady commit rhythm; files revisited and refined over time |

**Ownership & Iteration** is only assessable from git history — omit this
dimension from the skills matrix if git history was not available.

For soft skills, look for *consistency* across the codebase and history, not
isolated examples. One descriptive commit message doesn't make someone a strong
communicator; a consistent pattern across 50 commits does. A single data point
is insufficient — note it as "limited signal".

## Synthesize

Look for:

- **Confirmation** — git history and file analysis pointing to the same signal
  strengthens confidence significantly.
- **Contradiction** — clean files but messy commit history (or vice versa) is
  itself an interesting signal worth naming.
- **Recurring patterns** across multiple files → reliable signal.
- **One-offs** → interesting but exploratory; don't overweight.
- **Gaps** → absent things that would be expected given the stack.
- **The through-line** → the single characterization that ties it all together.
