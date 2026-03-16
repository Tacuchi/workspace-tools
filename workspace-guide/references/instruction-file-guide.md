# Project Instruction File Guide

The project instruction file can be `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md` depending on the user's CLI:

| CLI | Instruction file |
|-----|-----------------|
| Claude Code | `CLAUDE.md` |
| Gemini CLI | `GEMINI.md` |
| Codex, Warp, Crush, OpenCode | `AGENTS.md` |

## Rules

- Content is identical regardless of filename
- Keep it minimal: <200 lines
- Must contain: name, description, stack, commands, references to `docs/`
- When editing, find which file exists at project root and modify that one
- Do not create symlinks between instruction files

## Minimal Structure

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
- Numbered files: `NNN-name.ext`
- Include SKILL.md in tools
- Plans and decisions saved in docs/
```
