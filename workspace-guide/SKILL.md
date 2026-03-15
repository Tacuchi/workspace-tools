---
name: workspace-guide
description: >
  Workspace conventions for directory structure, file numbering, and tool organization.
  Auto-activates when the project uses a workspace layout with docs/, tools/, AGENTS.md,
  CLAUDE.md, GEMINI.md, or files matching NNN-*.ext pattern (e.g., 001-arquitectura.md).
  Guides the agent on where to place documents, plans, decisions, scripts, and skills.
  Ensures consistent numbering, proper SKILL.md creation, and minimal instruction files.
---

# Workspace Conventions

These conventions apply whenever you detect workspace markers in the project:
- Directories: `docs/`, `tools/`
- Instruction files: `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`
- Numbered files: `NNN-*.ext` pattern (e.g., `001-arquitectura.md`)

If any of these markers exist, follow all conventions below automatically.

---

## 1. When This Applies

Activate these conventions when you detect **any** of:
- `docs/` directory exists
- `tools/` directory exists
- `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md` at project root
- Files matching `NNN-nombre.ext` pattern (3-digit prefix)

You do NOT need the user to ask — apply conventions automatically.

---

## 2. Directory Structure

### docs/ — Project documentation

```
docs/
├── arquitectura/       ← architecture and design (mandatory)
├── planes/             ← work plans and specs
├── decisiones/         ← ADRs (Architecture Decision Records)
├── manuales/           ← installation, configuration, deployment guides
├── especificaciones/   ← functional and technical specs
└── scripts/            ← SQL, analysis scripts, DDL
    ├── ddl/
    └── analisis/
```

### tools/ — Scripts and skills

```
tools/
├── scripts/            ← executable code (Python, Bash, etc.) + SKILL.md
│   └── <tool-name>/
│       ├── SKILL.md
│       └── 001-script.sh
└── skills/             ← instruction-only (no executable code), SKILL.md only
    └── <skill-name>/
        └── SKILL.md
```

---

## 3. File Numbering

Format: `NNN-descriptive-name.ext`

- `NNN` = 3-digit sequence (001, 002, ..., 999)
- Preserves chronological creation order
- Files sort correctly with `ls`
- Context survives when switching between agents

Examples:
```
docs/planes/001-feature-login.md
docs/planes/002-refactor-auth.md
docs/decisiones/001-uso-angular-16.md
docs/scripts/ddl/001-create-tables.sql
```

When creating a new file in an existing directory, check the highest existing number and increment by 1.

---

## 4. Rules

- **No build/test** — do not execute build or test commands during editing. Wait for the user to request it.
- **No git** — do not make commits or any git operations.
- **Plans** — save work plans in `docs/planes/NNN-<plan>.md`.
- **Decisions** — save architectural decisions in `docs/decisiones/NNN-<decision>.md`.
- **SKILL.md in tools** — every tool in `tools/scripts/` or `tools/skills/` must have a SKILL.md.
- **SKILL.md in source** — SKILL.md can also exist inside `src/`, `lib/`, etc. when the user requests it.

---

## 5. Tool Creation Heuristic

When creating a new tool, decide its location:

| Type | Location | Contents |
|------|----------|----------|
| **Executable code** (scripts, CLIs, binaries) | `tools/scripts/<name>/` | SKILL.md + code files |
| **Instructions only** (guides, checklists, prompts) | `tools/skills/<name>/` | SKILL.md only (no code) |

Examples:
- Database migration script → `tools/scripts/db-migrate/` (has `.sh` files)
- Deploy guide with steps → `tools/skills/deploy/` (instructions only)
- Seed data generator → `tools/scripts/seed-data/` (has `.py` files)
- Testing checklist → `tools/skills/testing/` (instructions only)

---

## 6. Existing Tools

Before creating a new tool, check these locations for existing ones:

1. `tools/scripts/` — project executable tools
2. `tools/skills/` — project instruction skills
3. `.agents/skills/` — synced project skills
4. `.claude/skills/` — Claude-specific skills
5. `.gemini/skills/` — Gemini-specific skills

Do not create duplicates. If a similar tool exists, update it instead.

---

## 7. SKILL.md Format

Use the template in `references/skill-template.md` for creating new SKILL.md files.

### For tools/scripts/ (executable code)

```markdown
---
name: <tool-name>
description: |
  What this tool does (1-3 lines).
  When to use it.
---

# <tool-name>

## Requirements
- Runtime/dependencies needed

## Usage
\`\`\`bash
<command to run>
\`\`\`

## Files
- `001-file.ext` — what it does
- `002-file.ext` — what it does
```

### For tools/skills/ (instructions only)

```markdown
---
name: <skill-name>
description: |
  What this skill guides (1-3 lines).
  When to use it.
---

# <skill-name>

## Prerequisites
- What must be in place

## Steps
1. First step
2. Second step
3. Third step

## Notes
- Important considerations
```

---

## 8. Project Instruction File

The project instruction file can be `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md` depending on the user's CLI:

| CLI | Instruction file |
|-----|-----------------|
| Claude Code | `CLAUDE.md` |
| Gemini CLI | `GEMINI.md` |
| Codex, Warp, Crush, OpenCode | `AGENTS.md` |

**Rules for the instruction file:**
- Content is identical regardless of filename
- Keep it minimal: <200 lines
- Must contain: name, description, stack, commands, references to `docs/`
- When editing, find which file exists at project root and modify that one
- Do not create symlinks between instruction files

**Minimal structure:**

```markdown
# <Project Name>

<1-2 line description>

## Stack
- <language> <version>
- <framework> <version>

## Commands
- Dev: `<dev command>`
- Build: `<build command>`
- Test: `<test command>`

## Structure
> See docs/arquitectura/001-arquitectura.md

## Conventions
> See docs/decisiones/

## Rules
- Documents/artifacts: `docs/<topic>/`
- Tools/scripts: `tools/scripts/<tool>/`
- No build/test during editing
- No git commits
- Numbered files: `NNN-name.ext`
- Include SKILL.md in tools
- Plans and decisions saved in docs/
```

---

## 9. Related Tools

### workspace-setup (initial step)

If the project has a monolithic instruction file (>200 lines from `/init`), suggest:

> The instruction file is large. You can split it into `docs/arquitectura/` using workspace-setup:
> `npx skills add tacuchi/workspace-tools@workspace-setup`

### workspace-update (after creating tools)

After creating tools in `tools/scripts/` or `tools/skills/`, suggest syncing:

> New tools created. Sync SKILL.md to `.agents/skills/` with:
> `npx workspace-update sync`

This makes project tools discoverable by all compatible agents.
