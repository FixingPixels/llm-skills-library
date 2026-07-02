# LLM Skills Library

Reusable [Agent Skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) for Claude, Cursor, and other LLM coding assistants. Each skill is a self-contained package of routing instructions, workflows, and reference material that teaches an agent how to help with a specific domain.

Maintained by [Fixing Pixels](https://github.com/FixingPixels).

## Skills

| Skill | Description | Docs |
|-------|-------------|------|
| [**board-game-design**](board-game-design/) | Design partner for solo tabletop designers — concept through rulebook, playtesting, and art direction. | [README](board-game-design/README.md) |
| [**brainstorm-synthesis-portable**](brainstorm-synthesis-portable/) | Synthesizes a brainstorming session into a structured Idea Register — tags ideas by lens, scores rough viability, and surfaces cross-idea patterns. Writes files when a folder is mounted, falls back to inline output otherwise. | [README](brainstorm-synthesis-portable/README.md) |
| [**code-reflection**](code-reflection/) | Reads your codebase and commit history to profile how you build, then produces a sourced capability report and a prioritized growth plan. Ships two skills: `repo-capability-analyst` and `growth-planner`. | [README](code-reflection/README.md) |
| [**mobile-app-designer**](mobile-app-designer/) | Design partner for indie mobile apps — idea validation through UX, onboarding, visual design, stack, and monetization. | [README](mobile-app-designer/README.md) |
| [**voice-profile-generator**](voice-profile-generator/) | Builds and maintains a living voice profile from meeting transcripts and writing samples; drives drafting sessions with a feedback loop. | [README](voice-profile-generator/README.md) |
| [**ux-wireframing-engine**](ux-wireframing-engine/) | Turns PRDs, design specs, and API contracts into grayscale HTML/Tailwind wireframes with requirement traceability. | [SKILL.md](ux-wireframing-engine/SKILL.md) |

### Trigger examples

**board-game-design** — "I'm making a board game about cybernetic gardening", "Review my rules for a medium-weight Euro", "My blind playtest failed because end-game dragged"

**brainstorm-synthesis-portable** — "Summarize what we covered", "Capture these ideas", "What patterns are you seeing?", "Let's wrap up this session"

**code-reflection** — "Analyze this repo and tell me who I am as a builder", "Profile my codebase from my code and commits", "What should I work on next?"

**mobile-app-designer** — "I want to build an app that helps people track water intake", "Design an onboarding flow for a habit tracker", "Should this be a modal or a sheet?"

**voice-profile-generator** — "Build my voice profile from my Granola notes", "Get the latest meeting notes and update my voice profile", "Draft a LinkedIn post in my voice"

**ux-wireframing-engine** — "Turn this PRD into wireframes", "Build a dashboard layout from these API specs with REQ traceability"

## Commands

Reusable [Cursor commands](https://docs.cursor.com/context/commands) for repo maintenance and agent workflows. Copy a command file into your project's `.cursor/commands/` directory (or your user-level commands folder).

| Command | Description |
|---------|-------------|
| [**audit-ai-harness**](commands/audit-ai-harness.md) | Audits a repository's AI-first development setup (rules, skills, MCP, guardrails) and writes a sourced maturity report to `docs/ai-harness.md`. Read-only except for the report. |

**Trigger example** — "Audit this repo's AI harness", "Run an AI harness audit and write the report"

## Repository layout

Each skill lives in its own top-level directory:

```
llm-skills-library/
├── board-game-design/              # Multi-skill plugin (7 sub-skills + references)
├── brainstorm-synthesis-portable/  # Single skill (references) — portable Idea Register
├── code-reflection/                # Multi-skill package (2 sub-skills + references/templates)
├── commands/                       # Reusable Cursor commands
├── mobile-app-designer/            # Multi-skill plugin (7 sub-skills + references)
├── voice-profile-generator/        # Living profile skill (references + evals)
├── ux-wireframing-engine/          # Single-file skill
└── LICENSE
```

Larger skills follow a consistent internal structure:

```
skill-name/
├── SKILL.md                    # Tier-2 router — loaded when the skill activates
├── README.md                   # Human-facing overview (where present)
├── skills/                     # Sub-skill routing documents (multi-skill packages)
├── references/                 # Tier-3 material loaded on demand
├── evals/                      # Test prompts for regression checks (where present)
└── .claude-plugin/             # Plugin manifest for Cowork (where present)
```

Skills use progressive disclosure: YAML frontmatter in `SKILL.md` is always available; the body loads on activation; reference files load only when a workflow step needs them.

## Installation

How you install a skill depends on your assistant and whether the skill ships as a plugin.

### Claude Code (Cowork plugin manager)

These skills include a `.claude-plugin/plugin.json` manifest and can be installed through the Cowork plugin manager:

- `board-game-design`
- `mobile-app-designer`

### Claude Code (manual)

Copy or sync a skill directory into your Claude skills folder:

```bash
mkdir -p ~/.claude/skills/<skill-name>
rsync -a --delete \
  /path/to/llm-skills-library/<skill-name>/ \
  ~/.claude/skills/<skill-name>/
```

For **voice-profile-generator**, preserve your living profile on reinstall:

```bash
rsync -a --delete \
  --exclude='references/voice-profile.md' \
  /path/to/llm-skills-library/voice-profile-generator/ \
  ~/.claude/skills/voice-profile-generator/
```

See the [voice-profile-generator README](voice-profile-generator/README.md) for full install and usage details.

### Cursor

Add skills to your Cursor skills directory (user-level or project-level):

```bash
mkdir -p ~/.cursor/skills/<skill-name>
rsync -a /path/to/llm-skills-library/<skill-name>/ ~/.cursor/skills/<skill-name>/
```

Cursor discovers skills from `SKILL.md` frontmatter. Restart or reload the agent session after adding or updating a skill.

For commands, copy files from `commands/` into `.cursor/commands/` (project-level) or `~/.cursor/commands/` (user-level):

```bash
mkdir -p ~/.cursor/commands
cp /path/to/llm-skills-library/commands/*.md ~/.cursor/commands/
```

### Other assistants

Any tool that supports Agent Skills can consume the `SKILL.md` file and its linked references. Copy the skill directory wholesale, or point your assistant's skill loader at this repository.

## Authoring and testing

When editing a skill:

1. Keep `SKILL.md` focused — route to `skills/` and `references/` rather than inlining long content.
2. Put YAML `description` triggers in frontmatter so the skill activates on the right requests.
3. Run evals after substantive changes. Skills with an `evals/` directory (currently **voice-profile-generator**) include realistic test prompts for regression checks.

Skills in this library follow conventions from Anthropic's [skill authoring best practices](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices).

## License

MIT — see [LICENSE](LICENSE).

Copyright (c) 2026 Fixing Pixels
