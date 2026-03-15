# SKILL.md Template

Use these templates when creating SKILL.md files for tools.

---

## Variant 1: tools/scripts/ (executable code)

For tools that include runnable scripts, CLIs, or binaries.

```markdown
---
name: <tool-name>
description: |
  <What this tool does — 1-3 lines>
  <When to use it>
---

# <tool-name>

## Requirements
- <Runtime needed (e.g., Python 3.10+, Node 18+)>
- <Dependencies or access needed>

## Usage

\`\`\`bash
<command to run the tool>
\`\`\`

### Options
- `--flag` — description of flag
- `--other` — description of other flag

## Files
- `001-file.ext` — what this file does
- `002-file.ext` — what this file does

## Notes
- <Important caveats or gotchas>
```

### Example: seed-data

```markdown
---
name: seed-data
description: |
  Generates test data for the development environment.
  Creates sample users, products, and operations.
  Use when you need to populate the local database.
---

# seed-data

## Requirements
- Python 3.10+
- Access to local DB (see docs/manuales/002-configuracion.md)

## Usage

\`\`\`bash
python tools/scripts/seed-data/001-seed-users.py --env dev
\`\`\`

## Files
- `001-seed-users.py` — creates 10 test users
- `002-seed-products.sql` — inserts products and plans
```

---

## Variant 2: tools/skills/ (instructions only)

For skills that contain only guidance, checklists, or workflows — no executable code.

```markdown
---
name: <skill-name>
description: |
  <What this skill guides — 1-3 lines>
  <When to use it>
---

# <skill-name>

## Prerequisites
- <What must be in place before using this skill>

## Steps
1. <First step>
2. <Second step>
3. <Third step>

## Notes
- <Important considerations>
- <Common mistakes to avoid>
```

### Example: deploy

```markdown
---
name: deploy
description: |
  Step-by-step guide for deploying the application.
  Includes pre-deploy checklist and per-environment steps.
  Use when a manual deploy is needed.
---

# deploy

## Prerequisites
- Access to production cluster
- Environment variables configured (see docs/manuales/002-configuracion.md)

## Steps
1. Verify all tests pass
2. Create release tag
3. Run CI/CD pipeline
4. Verify deployment health checks

## Notes
- Always deploy to staging first
- Check monitoring dashboard after deploy
```

---

## Choosing the right variant

| Question | scripts/ | skills/ |
|----------|----------|---------|
| Has `.py`, `.sh`, `.sql`, or other executable files? | Yes | No |
| Can be run from the command line? | Yes | No |
| Is it purely a guide or checklist? | No | Yes |
| Does it generate output or modify state? | Yes | No |
