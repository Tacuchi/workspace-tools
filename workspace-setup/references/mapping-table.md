# Mapping Table: /init Sections → docs/ Destination

Detailed mapping for splitting the monolithic `/init` output into organized workspace files.

---

## Sections that STAY in the instruction file

These sections are short and essential for quick agent orientation:

| Section | Why it stays |
|---------|-------------|
| Project name and description | 1-2 lines, identity |
| Stack (language, framework, versions) | 3-5 lines, essential context |
| Build/dev/test commands | 3-5 lines, frequently needed |
| Basic rules | 5-10 lines, behavioral constraints |

---

## Sections that MOVE to docs/

### → docs/arquitectura/001-arquitectura.md

All structural and design information consolidates here:

| Section from /init | Example content |
|---|---|
| Architecture overview | "Monolithic Express app with layered architecture" |
| Folder structure | "src/controllers/, src/services/, src/models/" |
| Key services | "AuthService handles JWT, PaymentService wraps Stripe" |
| Shared components | "src/shared/utils/, src/shared/middleware/" |
| Feature module pattern | "Each feature in src/features/<name>/ with controller, service, model" |
| Database schema overview | "PostgreSQL with 15 tables, Prisma ORM" |
| State management | "Redux Toolkit with slice-per-feature pattern" |

**Example output file:**

```markdown
# Architecture

## Overview
Monolithic Express app with layered architecture...

## Folder Structure
\`\`\`
src/
├── controllers/
├── services/
├── models/
└── shared/
\`\`\`

## Key Services
- **AuthService** — JWT authentication and refresh tokens
- **PaymentService** — Stripe integration for subscriptions

## Feature Module Pattern
Each feature follows: controller → service → model
```

### → docs/especificaciones/001-api-patterns.md

API-specific patterns and conventions:

| Section from /init | Example content |
|---|---|
| API response patterns | "All endpoints return { data, error, meta }" |
| Error handling conventions | "AppError class with status codes" |
| Authentication flow | "Bearer token in Authorization header" |
| Validation patterns | "Zod schemas in src/validators/" |

### → docs/manuales/002-configuracion.md

Environment and configuration details:

| Section from /init | Example content |
|---|---|
| Environment variables | "DATABASE_URL, JWT_SECRET, STRIPE_KEY" |
| Configuration files | ".env.local, .env.production" |
| Local setup steps | "docker-compose up, npm run migrate" |
| External service connections | "Redis on port 6379, PostgreSQL on 5432" |

---

## Decision guide

When unsure where a section belongs:

| If the content is about... | Put it in... |
|---|---|
| How the code is organized | `docs/arquitectura/001-arquitectura.md` |
| How APIs behave | `docs/especificaciones/001-api-patterns.md` |
| How to set up or configure | `docs/manuales/002-configuracion.md` |
| How to run commands | Instruction file (stays) |
| What tech stack is used | Instruction file (stays) |

If a section doesn't clearly fit any destination, keep it in `docs/arquitectura/001-arquitectura.md` as the default catch-all for structural documentation.
