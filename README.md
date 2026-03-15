# workspace-tools

Agent skills for workspace conventions and architecture setup.

## Skills

### workspace-guide (pushy)

Auto-activating skill that teaches agents workspace conventions: directory structure (`docs/`, `tools/`), file numbering (`NNN-nombre.ext`), tool creation heuristics (scripts vs skills), and project instruction file management.

Activates automatically when workspace markers are detected (`docs/`, `tools/`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `NNN-*.ext` files).

```bash
npx skills add tacuchi/workspace-tools@workspace-guide
```

### workspace-setup (on-demand)

On-demand skill that splits the monolithic `/init` output into organized `docs/arquitectura/` files. Reduces instruction file size to <200 lines for optimal agent adherence.

Invoke with phrases like "setup", "empieza con la arquitectura", "separa el init", "split the init".

```bash
npx skills add tacuchi/workspace-tools@workspace-setup
```

## Companion tool

After creating tools in `tools/scripts/` or `tools/skills/`, use [workspace-update](https://github.com/tacuchi/workspace-update) to sync SKILL.md files to `.agents/skills/`:

```bash
npx workspace-update sync
```

## Compatibility

Works with any agent that supports the [Agent Skills](https://skills.sh/) standard, including:

- [Warp](https://www.warp.dev/)
- [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code)
- [Cursor](https://www.cursor.com/)
- [Windsurf](https://windsurf.com/)
- [GitHub Copilot](https://github.com/features/copilot)

## License

[MIT](LICENSE)
