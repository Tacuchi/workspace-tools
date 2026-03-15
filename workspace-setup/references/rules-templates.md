# Conditional Rules Templates

Templates for `.claude/rules/<tech>.md` files. These are extracted during workspace-setup
when `--agent claude` is specified. Each file uses frontmatter globs so Claude Code only
loads the rules when editing matching files.

---

## TypeScript

**File:** `.claude/rules/typescript.md`

```markdown
---
globs: ["src/**/*.ts", "src/**/*.tsx"]
---

- Use strict TypeScript — no `any` unless explicitly justified
- Prefer `interface` over `type` for object shapes
- Use `readonly` for properties that should not be mutated
- Prefer `unknown` over `any` for untyped values, then narrow with type guards
- Use barrel exports (`index.ts`) only at module boundaries, not within features
- Prefer named exports over default exports
- Error handling: use custom error classes extending `Error`
```

---

## Java

**File:** `.claude/rules/java.md`

```markdown
---
globs: ["src/**/*.java"]
---

- Follow existing package naming conventions in the project
- Use constructor injection over field injection for dependencies
- Prefer `Optional` return types over null for methods that may not return a value
- Use `final` for variables that should not be reassigned
- Prefer streams over imperative loops for collection operations
- Use `@Override` annotation on all overridden methods
- Exception handling: catch specific exceptions, never catch `Exception` or `Throwable` broadly
```

---

## SQL

**File:** `.claude/rules/sql.md`

```markdown
---
globs: ["**/*.sql", "docs/scripts/**/*.sql"]
---

- Use uppercase for SQL keywords (SELECT, FROM, WHERE, JOIN)
- Use snake_case for table and column names
- Always specify column names in INSERT statements — no `INSERT INTO table VALUES`
- Use parameterized queries — never concatenate user input into SQL strings
- Include comments for complex queries explaining the business logic
- Prefer explicit JOINs over implicit (comma-separated FROM)
```

---

## Angular

**File:** `.claude/rules/angular.md`

```markdown
---
globs: ["src/**/*.ts", "src/**/*.html", "src/**/*.scss"]
---

- Follow the Angular style guide for file naming: `feature.type.ts`
- Use standalone components (Angular 14+) unless the project uses NgModules
- Prefer signals over RxJS for simple state when using Angular 16+
- Use `trackBy` in `*ngFor` directives for performance
- Keep templates under 50 lines — extract to child components if larger
- Use reactive forms over template-driven forms for complex forms
```

---

## React

**File:** `.claude/rules/react.md`

```markdown
---
globs: ["src/**/*.tsx", "src/**/*.jsx"]
---

- Use functional components with hooks — no class components
- Prefer named exports for components
- Keep components under 150 lines — extract subcomponents if larger
- Use custom hooks to extract reusable logic from components
- Memoize expensive computations with `useMemo` and callbacks with `useCallback`
- Colocate component files: `Component.tsx`, `Component.test.tsx`, `Component.module.css`
```

---

## Usage notes

- Extract only rules relevant to the project's detected stack
- Create at most 2-3 rule files to avoid fragmentation
- Each file should be <30 lines (excluding frontmatter)
- Globs must match actual project file paths
- These rules complement (not replace) the main instruction file rules
