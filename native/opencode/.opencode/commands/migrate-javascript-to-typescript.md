---
description: Plans and carries out an incremental JavaScript-to-TypeScript migration with config, file order, typed boundaries and a strictness ratchet. Use to move a JS codebase without a freeze.
---

# Migrate JavaScript to TypeScript

## Inputs

- [REPO_AREA] (required): The package, folder or app to migrate, and any constraints (release dates, files owned by other teams, code that must not change).
- [STRICTNESS_TARGET] (optional; one of: loose, strict; default: strict): Where the type checker should end up - loose (strict off, catch obvious errors) or strict (the full strict family of flags).

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Big-bang TypeScript migrations stall: hundreds of files renamed at once, `any` sprinkled everywhere to get the build green, behaviour changes hidden in "type fixes", and a strict mode that is never turned on. Migrations that finish are incremental. JavaScript and TypeScript coexist, the most valuable boundaries are typed first, each batch is small and reviewable, and a CI guard makes the type safety only ever go up.
</context>

<task>
Migrate [REPO_AREA] to TypeScript, targeting [STRICTNESS_TARGET] type checking.

Phase 1, plan (no file changes yet):
1. Inspect the build: bundler or compiler, Babel or SWC usage, test runner, linter, module system (ESM or CommonJS), Node version, path aliases, and any existing JSDoc types or `.d.ts` files. Run the build and tests and record the baseline results.
2. Propose the `tsconfig.json`: `allowJs` on and `checkJs` off to start, `noEmit` if a bundler compiles, `module` and `moduleResolution` matching the runtime (`NodeNext` for Node, `Bundler` for bundled apps), `isolatedModules`, `skipLibCheck`, and the target. Wire type checking into CI and the test runner.
3. Order the conversion: shared types and module boundaries first (API clients, data models, configuration, the most-imported utilities), then leaf modules up the dependency graph. Group files into batches of about 10 to 20 that can each merge on their own.
4. Define the strictness ratchet. For strict: turn on `strict` early and track each suppression (`any`, `@ts-expect-error`) with a count that CI only allows to go down. For loose: turn on `noImplicitAny` and `strictNullChecks` per directory as batches finish, and stop there.
5. List untyped dependencies and whether `@types` packages exist; plan small local declaration files for the rest.

Stop after Phase 1 and wait for approval.

Phase 2, after approval:
6. Convert one batch at a time, starting with the first: rename each file with `git mv` so history follows, then add types derived from how the code is actually used (parameters, return types of exported functions, shared shapes as named types), using existing JSDoc as a starting point. Use `unknown` rather than `any` at external inputs and narrow it with runtime validation, and change no runtime behaviour.
7. After each batch, run the type checker, the tests and the linter, and report the real results. Fix the types, not the behaviour.
</task>

<constraints>
- Never mix behaviour changes into a conversion batch. If typing reveals a bug, record it under Bugs found and leave the behaviour as it is, unless the user asks you to fix it.
- Do not silence errors with `any` without counting it in the ratchet and adding a `// TODO(types): reason` comment. Use `@ts-expect-error` with a reason instead of `@ts-ignore`, and do not use non-null assertions only to silence errors.
- Keep module paths and public exports stable so callers outside the migrated area keep working.
- Prefer inferred types over annotations that repeat what the compiler already knows.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Current state
Build, modules, test runner, file counts, and existing types.
## Config
The `tsconfig.json` and the build, test and CI changes, as diffs.
## Conversion order
A table: batch, files, why this order, estimated effort.
## Strictness ratchet
Flags by stage, the suppression budget, and the CI guard.
## Progress
(Phase 2 only) Table: batch, files, type check result, tests result, lint result, against the baseline.
## Escape hatches
(Phase 2 only) Bullets: `path:line` — `any` or `@ts-expect-error` — reason. Or "None".
## Bugs found
(Phase 2 only) Bullets: `path:line` — the bug — how it would surface. Not fixed. Or "None".
## Risks
Bullets: build tooling, runtime differences, and team habits to watch.
</output_format>

Arguments: $ARGUMENTS
