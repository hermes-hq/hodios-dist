---
name: migrate-js-to-typescript
description: Migrates a JavaScript codebase or folder to TypeScript incrementally, leaf modules first, with real types instead of any and no behaviour changes. Use when adopting TypeScript in an existing project.
license: CC0-1.0
arguments:
  - scope
  - strictness
argument-hint: <scope> [strictness]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: migration
  source: https://hermes-ide.com/prompts/migrate-js-to-typescript
  catalog: 2026.1002.1
---

# Migrate JavaScript to TypeScript

## Inputs

- `scope` (required): What to migrate, for example a folder, a package or the whole repository.
- `strictness` (optional; one of: gradual, strict; default: gradual): gradual starts loose and tightens at the end; strict uses strict mode for every migrated file from the start.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A TypeScript migration pays off only if the types are real. Renaming files and adding `any` everywhere gives the cost of TypeScript without the safety. Migrating leaf modules first means each file can be typed against already-typed dependencies, and keeping behaviour identical means any test failure points at a typing mistake, not a feature change.
</context>

<task>
Migrate $scope to TypeScript with $strictness strictness.

1. Inspect the setup: build tool, bundler, test runner, linter, module format, and any existing `tsconfig.json`. Run the build and tests and record the baseline.
2. Set up TypeScript so JavaScript and TypeScript can coexist (for example `allowJs`), matching the existing module format and paths. With strict strictness, enable `strict` now; with gradual, start with `strict` off and note the flags to turn on later.
3. Build the import graph for the scope and order files leaf first: files that import nothing internal come first.
4. Migrate in batches of up to about 10 files. For each file, rename it with `git mv` to keep history, then add types derived from how the code is actually used: parameters, return types of exported functions, and shared shapes as named types. Use existing JSDoc as a starting point. For third-party packages, install their type packages or write a minimal local declaration.
5. After each batch, run the type check and the tests. Fix the types, not the behaviour.
6. With gradual strictness, turn on the strict flags one at a time once everything is migrated, and fix what each one finds.
</task>

<constraints>
- No behaviour changes. If typing reveals a bug, record it under Bugs found and leave the behaviour as it is, unless the user asks you to fix it.
- Avoid `any`. When it is unavoidable, add `// TODO(types): reason` next to it, and list every instance under Escape hatches.
- Use `@ts-expect-error` with a reason instead of `@ts-ignore`, and do not use non-null assertions only to silence errors.
- Keep module paths and the public exports stable so callers outside the scope keep working.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Plan
The setup changes and the batches in order.
## Progress
Table: batch, files, type check result, tests result.
## Escape hatches
Bullets: `path:line` — `any` or `@ts-expect-error` — reason. Or "None".
## Bugs found
Bullets: `path:line` — the bug — how it would surface. Not fixed. Or "None".
## Verification
Commands run with their real results, before and after.
</output_format>
