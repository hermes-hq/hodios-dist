---
name: implement-feature-from-spec
description: Turns a written spec or ticket into working code that follows the codebase's patterns, with tests and a list of decisions. Use when handing a well-scoped ticket to an agent.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/implement-feature-from-spec
  catalog: 2026.1003.0
---

# Implement a feature from a spec

## Inputs

- [SPEC] (required): The ticket, spec or user story, including acceptance criteria if it has them.
- [SCOPE_PATHS] (optional): Files, folders or modules the change may touch. Leave empty to let the agent find the smallest set.
- [TEST_POLICY] (optional; one of: add-tests, update-existing, none; default: add-tests): add-tests: cover each acceptance criterion. update-existing: only adjust tests the spec changes. none: leave tests alone.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are implementing a ticket in an existing codebase you did not write. The person who handed it over will judge the result on four things: every acceptance criterion is met, the new code reads like the code around it, the tests would catch a regression, and nothing outside the ticket changed by surprise. A working change that ignores local conventions, or quietly decides an ambiguous requirement, costs them more review time than it saves.
</context>

<task>
Implement this spec:

[SPEC]

Allowed scope: [SCOPE_PATHS] (if empty, find the smallest set of files that delivers the spec).
Test policy: [TEST_POLICY].

1. **Pin down the requirements.** Rewrite the spec as numbered acceptance criteria. Add the requirements it implies but does not state (error cases, empty input, permissions, existing callers). List every ambiguity.
   - If an ambiguity changes a public API, data model, persisted format, permission or user-visible behaviour, stop and ask up to 5 numbered questions, each with the option you would pick by default. Write no code until answered.
   - If it is minor, choose the most conservative reading that matches existing behaviour, and record it under Decisions.
2. **Read before writing.** Find the entry point, the closest existing feature that does something similar, and the local conventions: error handling, validation, logging, naming, dependency injection, configuration, and test layout and runner. Use the analogous feature as your template.
3. **Plan.** List the files you will change or create, in order. If something outside the allowed scope must change, say why before changing it.
4. **Implement** in small, coherent steps. Reuse existing helpers instead of writing new ones. Add no new dependency unless the spec requires it; if it does, ask first.
5. **Test** according to the policy:
   - `add-tests`: at least one test per acceptance criterion, plus the failure or edge case that matters most for each, in the existing framework and style.
   - `update-existing`: change only the tests whose expected behaviour the spec changes. Add none.
   - `none`: do not touch tests. List the tests you would have written under Follow-ups.
6. **Verify.** Run the project's type check, linter and the relevant tests. Fix failures your change caused. Report failures that existed before you started without fixing them.
</task>

<constraints>
- Match the existing style even where you would choose differently. No drive-by refactors, renames or reformatting.
- Never mark a criterion "done" unless code implements it and a test or a run demonstrates it.
- Do not add feature flags, configuration options or abstractions the spec does not ask for.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Summary
Two or three sentences: what now works that did not before.

## Acceptance criteria
| # | Criterion | Status (done / partial / not done) | Where (`path:symbol`) | Test |

## Changes
One line per file: `path`, what changed and why.

## Decisions
Each interpretation or design choice you made: the choice, the alternative, and why. Mark the ones the requester should confirm with **confirm**.

## Verification
Each command you ran and its actual result (pass/fail counts, errors). Say plainly if you could not run something.

## Follow-ups
Out-of-scope issues you noticed, one line each, or "None".
</output_format>
