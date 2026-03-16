# Minimal Instruction File Template

The filename depends on `--agent` parameter (AGENTS.md, CLAUDE.md, or GEMINI.md).

## Template

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
<!-- Gemini CLI: use @docs/arquitectura/001-arquitectura.md -->

## Conventions
> See docs/decisiones/
<!-- Gemini CLI: use @docs/decisiones/ -->

## Rules
- Documents and artifacts go in `docs/<topic>/`
- Tools and scripts go in `tools/scripts/<tool>/` or `tools/skills/<skill>/`
- Do not execute build or tests during editing — wait for user request
- Do not make commits or git operations
- Use numbered files: `NNN-descriptive-name.ext`
- Include SKILL.md when creating tools
- Save plans in `docs/planes/` and decisions in `docs/decisiones/`
```

**Target:** <200 lines total (ideally ~50-80 lines). No architecture details, API patterns, or config details — those live in `docs/`.
