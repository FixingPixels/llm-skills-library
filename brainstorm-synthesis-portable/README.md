# Setup — Brainstorm Synthesis (Portable)

This skill works in two tiers (see `SKILL.md`):

- **Standalone** — no setup. Drop the skill in and it outputs an Idea Register inline in chat.
- **Folder** — point Claude at any working directory and it writes a `raw/` log plus a single `brainstorm-YYYY-MM-DD.md` register file.

This portable edition stays lightweight on purpose: it captures a raw log and a structured register, nothing more.

> **Want the full LLM-wiki experience?** If you want a compounding, cross-linked second brain — idea pages, theme pages, pattern pages, an `index.md`, and an activity log that build up across sessions — use [idea-distillery](https://github.com/FixingPixels/idea-distillery). It's an Obsidian vault + Claude skill that maintains the full Karpathy-style LLM wiki for you.

---

## Installing the skill

Place the `brainstorm-synthesis-portable/` folder (this whole directory, including `references/`) into your skills location:

- Claude Code / Cowork: `.claude/skills/brainstorm-synthesis-portable/`
- Cursor: `.cursor/skills/brainstorm-synthesis-portable/`

The skill is self-contained and does **not** depend on any project-level `CLAUDE.md` or wiki schema.

---

## Folder mode (Claude Cowork Project)

Cowork **Projects** (Claude desktop, Cowork mode) give the skill a persistent local working directory, which is all Folder mode needs.

1. Open the **Claude desktop app** and switch to **Cowork** mode in the left sidebar.
2. Click **+ New Project**.
3. Choose **"Start from scratch"** (new folder) or **"Use an existing folder"**.
4. **Name the project differently from the folder.** ⚠️ There is a known Cowork bug where a project name that matches the folder name mounts an empty nested subfolder (e.g. `MyNotes/MyNotes/`) and the agent reports the folder as empty. After creating the project, verify the mount points at the folder with your content, not an empty subfolder.
5. Install the `brainstorm-synthesis-portable` skill into the project (see above).
6. Brainstorm. When you say "wrap up this session" / "capture these ideas," the skill detects the mounted folder and writes the raw log and register.

### Important caveat: Dispatch sessions

Cowork **Dispatch** tasks run in isolated sessions that **do not inherit** the parent project's mounted folder or memory. A dispatched run will report `User selected a folder: no` and fall back to Standalone mode. **Run synthesis from the main project session**, not a dispatched task, until this is addressed upstream.

---

## Verifying the tier

Ask Claude to "wrap up this session" and watch where output lands:

- A `raw/` log and a single `brainstorm-YYYY-MM-DD.md` register → **Folder mode** ✅
- The register prints in the chat with no files written → **Standalone mode**

If you expected Folder mode but got Standalone mode, the working directory isn't being detected — confirm a folder is mounted, and that you're not in a Dispatch session.
