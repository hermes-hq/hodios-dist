---
name: adopt-strict-typing-track
description: Moves a Python or TypeScript codebase to strict type checking one module at a time, fixing real bugs found and ratcheting config so coverage never slides back. Use to adopt strict mode safely.
license: CC0-1.0
arguments:
  - language
  - type_check_command
  - first_module
  - test_command
argument-hint: "[language] <type_check_command> [first_module] [test_command]"
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: migration
  source: https://hermes-ide.com/prompts/adopt-strict-typing-track
  catalog: 2026.1004.3
---

# Adopt strict type checking module by module

## Inputs

- `language` (optional; one of: python, typescript; default: typescript): The language of the codebase.
- `type_check_command` (required): The command that runs the type checker today, for example "npx tsc --noEmit", "mypy src" or "pyright".
- `first_module` (optional): The module or directory to convert first. Leave empty and step 1 picks one from the bottom of the import graph with few errors.
- `test_command` (optional; default: the project's documented test command): The command that runs the tests, so each module's changes are proven not to alter behaviour.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Adopts strict type checking in this $language codebase without a big-bang change. Turning strict on for the whole project at once produces thousands of errors, and teams answer with blanket suppressions that hide the bugs strict mode exists to find. This track measures first, installs a ratchet that fits the checker, so strict coverage can only grow, then converts one module at a time from the bottom of the import graph up, stopping after each for review.

Rules for every step:
- The type checker run with `$type_check_command` and the tests, run with $test_command, are the only evidence. Report real error counts, never estimates.
- A type change must not change runtime behaviour. When strict mode exposes a real bug (a possible None, a wrong argument, an unhandled union member), record it separately; fix it only when the fix is small and covered by a test, and list it either way.
- Suppressions are a last resort: `any`, `as` casts, non-null assertions, `# type: ignore`, `cast()` and `@ts-ignore` each need a one-line reason next to them and are counted in every report. Prefer `@ts-expect-error` and error-code-specific `# type: ignore[code]` so they fail once they are no longer needed.
- Do not edit generated code or vendored code; exclude it from the checker instead and say so.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.

## Steps

Work through these steps in order. Do not skip a gate.

1. baseline (plan)
2. ratchet (build)
3. convert-module (build)
4. report (verify)

### Step 1: Measure and design the ratchet

1. Run `$type_check_command` and record the error count. Read the checker config: every tsconfig with its `extends` chain and references, or the mypy and pyright settings, including existing overrides and excludes.
2. Without changing the committed config, run the checker once with strict settings in a scratch config and count errors by file, directory and error code. TypeScript: the `strict` family, with `noUncheckedIndexedAccess` reported separately as optional. Python: mypy `--strict` or pyright `strict`, plus third-party packages without types or stubs.
3. Order modules bottom up from the internal import graph: modules that import few other internal modules first, since typing them gives everything above precise types. Within a level, fewer errors first; flag high-risk modules (money, auth, data writes) for extra test attention. Start with $first_module if given, and say if it sits high in the graph.
4. Design a ratchet that fails CI when a converted module gains a strict error, the converted set shrinks, or the suppression count grows:
   - TypeScript: `tsc` checks every file reachable through imports, so a second tsconfig with a growing `include` list also reports errors in unconverted imported files. Instead, run strict over the project and fail only on diagnostics in files on a committed list (a small filter script or an established strict-files tool), keep a per-file error baseline that may only fall, or use a strict tsconfig per package where project references already exist.
   - mypy: `strict` is global only and ignored in per-module sections. Prefer `strict = true` globally with one override listing unconverted modules and the individual strict flags turned off, so new code starts strict and the list only shrinks; otherwise enable the individual flags per converted module.
   - pyright: grow the `strict` path list, or set strict globally and list unconverted paths under a weaker mode.
5. Plan stubs: community stub packages to add, and local minimal stubs or targeted per-package ignores for the rest, never a global `ignore_missing_imports` or `skipLibCheck` change made to hide errors.

Write the artifact: Baseline, Strict cost (Module | Errors | Top error codes | Imports | Imported by), Order, Ratchet design and CI command, Stubs. Stop and wait for approval.

Save this step's result to `strict-typing/01-baseline.md`.

**Gate:** stop here and wait for the user's approval before step 2 (ratchet).

### Step 2: Install the ratchet

1. Add the approved strict configuration, starting with only modules that already pass strict (or, inverse design, with every other module listed as unconverted).
2. Wire the strict check into the project's scripts or task runner and into CI next to the existing type check.
3. Add a suppression counter for converted modules (`any`, non-null assertions, `@ts-ignore`, `@ts-expect-error`, `# type: ignore`, `cast(`) compared with a committed number that may only go down.
4. Prove the ratchet bites: in a scratch change, add one strict error and one suppression to a converted file, confirm the check fails for each, then revert.
5. Run `$type_check_command`, the strict check and the tests. All must pass before any module is converted.

Continue to step 3.

### Step 3: Convert one module (repeat per module)

Take the next module in the approved order.

1. Move the module onto the strict side of the ratchet (add it to the strict list, or remove it from the unconverted list) and run the strict check to list its errors in that module only.
2. Fix them in this order of preference: correct annotations on public functions and exported types; narrowing (type guards, `isinstance`, discriminated unions, early returns) instead of casts; `unknown` plus validation at untyped boundaries such as JSON parsing, environment variables and third-party responses; an explicit annotation at the boundary when a loose type comes from a module not yet converted; stubs for untyped dependencies; a counted, commented suppression only when none of these work.
3. When an error is a real bug, add it to the bug list with file and line, what could go wrong at runtime, and whether you fixed it (with the covering test) or left it for a decision.
4. Run the strict check, `$type_check_command` and the tests. All must pass, and the suppression count must not exceed the step 2 baseline plus the documented new ones.

Append to the module log: Module | Errors fixed | Suppressions added (with reasons) | Bugs found | Checks run and results. Stop and wait for approval before the next module. If the user approves a batch of modules at once, still run all checks and log each module separately.

Save this step's result to `strict-typing/03-module-log.md`.

**Gate:** stop here and wait for the user's approval before step 4 (report).

### Step 4: Report

Write the report with these sections:

#### Coverage
Modules under strict before and after, as counts and as a share of source files, from the real config.

#### Bugs found
Table: File and line | Risk at runtime | Fixed (with test) or open.

#### Suppressions
Count before and after, and every new suppression with its reason.

#### Ratchet
How the CI check works and how a developer adds a module.

#### Next modules
The remaining order with each module's measured strict error count.

#### Checks
The commands run in this step and their real results.

Save this step's result to `strict-typing/04-report.md`.
