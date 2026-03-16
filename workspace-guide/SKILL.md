---
name: workspace-guide
description: >
  Workspace conventions for directory structure, file numbering, and tool organization.
  Auto-activates when the project uses a workspace layout with docs/, tools/, AGENTS.md,
  CLAUDE.md, GEMINI.md, or files matching NNN-*.ext pattern (e.g., 001-arquitectura.md).
  Guides the agent on where to place documents, plans, decisions, scripts, and skills.
  Ensures consistent numbering, proper SKILL.md creation, and minimal instruction files.
  Does NOT activate in repos without these workspace markers.
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

## 2. Where Does This Go?

| What are you creating? | Destination |
|---|---|
| Architecture/design documentation | `docs/arquitectura/NNN-<name>.md` |
| Work plan or analysis | `docs/planes/NNN-<name>.md` |
| Architecture Decision Record | `docs/decisiones/NNN-<name>.md` |
| Manual, setup, or config guide | `docs/manuales/NNN-<name>.md` |
| Functional/technical spec | `docs/especificaciones/NNN-<name>.md` |
| SQL script or data analysis | `docs/scripts/<topic>/NNN-<name>.sql` |
| Executable tool (scripts, CLIs) | `tools/scripts/<name>/` (with SKILL.md) |
| Instruction-only guidance | `tools/skills/<name>/` (SKILL.md only) |

---

## 3. Directory Structure

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

## 4. File Numbering

Format: `NNN-descriptive-name.ext`

- `NNN` = 3-digit sequence (001, 002, ..., 999)
- Preserves chronological creation order
- Files sort correctly with `ls`

When creating a new file, MUST check the highest existing number in the target directory (`ls docs/<subdir>/`) and increment by 1.

---

## 5. Rules

- **Plans** — save work plans in `docs/planes/NNN-<plan>.md`.
- **Decisions** — save architectural decisions in `docs/decisiones/NNN-<decision>.md`.
- **SKILL.md in tools** — every tool in `tools/scripts/` or `tools/skills/` MUST have a SKILL.md.
- **SKILL.md in source** — SKILL.md can also exist inside `src/`, `lib/`, etc. when the user requests it.

---

## 6. NEVER Do This

- NEVER create unnumbered files in docs/ — breaks chronological ordering, causes confusion when switching agents
- NEVER put executable code in tools/skills/ — skill discovery treats skills/ as instruction-only; executables won't be found by runners
- NEVER create a SKILL.md without a description in frontmatter — the tool becomes invisible to all agent skill discovery systems
- NEVER duplicate content between the instruction file and docs/ — creates drift; instruction file should only reference docs/
- NEVER create docs/planes/ or docs/decisiones/ during initial setup — they fill on demand; empty dirs clutter the workspace
- NEVER create a numbered file without checking the current highest number (`ls docs/<subdir>/` first)
- NEVER use a number already taken — always increment from the highest existing number

---

## 7. Tool Creation Heuristic

When creating a new tool, decide its location:

| Type | Location | Contents |
|------|----------|----------|
| **Executable code** (scripts, CLIs, binaries) | `tools/scripts/<name>/` | SKILL.md + code files |
| **Instructions only** (guides, checklists, prompts) | `tools/skills/<name>/` | SKILL.md only (no code) |

---

## 8. Existing Tools

Before creating a new tool, check these locations for existing ones:

1. `tools/scripts/` — project executable tools
2. `tools/skills/` — project instruction skills
3. `.agents/skills/` — synced project skills
4. `.claude/skills/` — Claude-specific skills
5. `.gemini/skills/` — Gemini-specific skills

Do not create duplicates. If a similar tool exists, update it instead.

---

## 9. SKILL.md and Instruction Files

> When creating a tool, follow `references/skill-template.md`

> For instruction file format, see `references/instruction-file-guide.md`

---

## 10. Related Tools

### workspace-setup (initial step)

If the project has a monolithic instruction file (>200 lines from `/init`), suggest:

> The instruction file is large. You can split it into `docs/arquitectura/` using workspace-setup:
> `npx skills add tacuchi/workspace-tools@workspace-setup`

### workspace-update (after creating tools)

After creating tools in `tools/scripts/` or `tools/skills/`, suggest syncing:

> New tools created. Sync SKILL.md to `.agents/skills/` with:
> `npx workspace-update sync`

This makes project tools discoverable by all compatible agents.
