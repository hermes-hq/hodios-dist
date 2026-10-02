---
name: extract-module
description: Moves one responsibility out of a large file or class into its own module in small, test-verified steps, without changing behaviour or the public API. Use when a file does too many things.
license: CC0-1.0
arguments:
  - source
  - responsibility
  - destination
argument-hint: <source> <responsibility> [destination]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/extract-module
  catalog: 2026.1002.1
---

# Extract a module

## Inputs

- `source` (required): The file, class or module to extract from.
- `responsibility` (required): What to extract, for example "the CSV export logic" or "everything that talks to the payment provider".
- `destination` (optional): Where the new module should live. Leave empty to follow the project's layout conventions.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Extracting a module is a refactor: the program must behave the same before and after. The hard parts are choosing a boundary that leaves both sides cohesive, and moving the code without breaking callers, creating import cycles or quietly changing behaviour along the way.
</context>

<task>
Extract $responsibility from $source into its own moduleOnly if destination was provided:  at $destination.
1. **Check the safety net.** Find the tests that cover the code to move. If coverage is thin, stop and report which behaviours need tests first. Do not refactor untested code silently.
2. **Draw the boundary.** List the functions, types and state that belong to the responsibility, and everything they use from the rest of the file. Choose the boundary that minimises what crosses it. If the responsibility shares mutable state with the rest of the file, say how you will pass it explicitly.
3. **Move in small steps**, running the tests after each:
   1. create the new module and move the code unchanged;
   2. import it back into the original file, re-exporting what external callers use so they keep working;
   3. update internal callers to import from the new module;
   4. remove the re-exports only if every caller is in this repository and has been updated. For a public library API, keep them and mark them deprecated.
4. Check for import cycles and fix them by moving the shared piece, not by lazy imports.
5. Run the full test suite, the type checker and the linter.
</task>

<constraints>
- No behaviour changes: no bug fixes, renames of public symbols, signature changes or "improvements" inside moved code. List those under follow-ups instead.
- Keep the diff reviewable: moved code should appear as a move, not a rewrite.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Boundary
What moved, what stayed, and what crosses the boundary, in a short list.
## Steps
The steps you took, each with its test result.
## Diff
The full diff.
## Verification
Test, type-check and lint commands with results.
## Follow-ups
Improvements you noticed but did not make, or "None".
</output_format>
