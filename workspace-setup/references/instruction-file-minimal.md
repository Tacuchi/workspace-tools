# Minimal Instruction File Template

This is the target format for the instruction file after workspace-setup splits the content.
The filename depends on the `--agent` parameter (AGENTS.md, CLAUDE.md, or GEMINI.md).

---

## Template (AGENTS.md / CLAUDE.md)

```markdown
# <Project Name>

<1-2 line description of the project>

## Stack
- <language> <version>
- <framework> <version>
- <database> (if applicable)
- <key dependencies>

## Commands
- Dev: `<dev command>`
- Build: `<build command>`
- Test: `<test command>`
- Lint: `<lint command>` (if applicable)

## Structure
> See docs/arquitectura/001-arquitectura.md

## Conventions
> See docs/decisiones/

## Rules
- Documents and artifacts go in `docs/<topic>/`
- Tools and scripts go in `tools/scripts/<tool>/` or `tools/skills/<skill>/`
- Do not execute build or tests during editing — wait for user request
- Do not make commits or git operations
- Use numbered files: `NNN-descriptive-name.ext`
- Include SKILL.md when creating tools
- Save plans in `docs/planes/` and decisions in `docs/decisiones/`
```

---

## Template (GEMINI.md)

Same content but references use Gemini CLI's native `@import` syntax:

```markdown
# <Project Name>

<1-2 line description of the project>

## Stack
- <language> <version>
- <framework> <version>
- <database> (if applicable)
- <key dependencies>

## Commands
- Dev: `<dev command>`
- Build: `<build command>`
- Test: `<test command>`

## Structure
@docs/arquitectura/001-arquitectura.md

## Conventions
@docs/decisiones/

## Rules
- Documents and artifacts go in `docs/<topic>/`
- Tools and scripts go in `tools/scripts/<tool>/` or `tools/skills/<skill>/`
- Do not execute build or tests during editing — wait for user request
- Do not make commits or git operations
- Use numbered files: `NNN-descriptive-name.ext`
- Include SKILL.md when creating tools
- Save plans in `docs/planes/` and decisions in `docs/decisiones/`
```

---

## Guidelines

- **Target:** <200 lines total (ideally ~50-80 lines)
- **No architecture details** — those live in `docs/arquitectura/`
- **No API patterns** — those live in `docs/especificaciones/`
- **No config details** — those live in `docs/manuales/`
- **Keep commands** — agents need these frequently
- **Keep rules** — behavioral constraints must be immediately visible
