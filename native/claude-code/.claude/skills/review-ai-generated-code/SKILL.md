---
name: review-ai-generated-code
description: Reviews code written by an AI assistant for hallucinated APIs, over-engineering, swallowed errors, weakened tests and copy-paste drift. Use before merging a change an agent produced.
license: CC0-1.0
arguments:
  - diff
  - task_description
argument-hint: <diff> [task_description]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: code-review
  source: https://hermes-ide.com/prompts/review-ai-generated-code
  catalog: 2026.1004.3
---

# Review AI-generated code

## Inputs

- `diff` (required): The unified diff or changed files the assistant produced.
- `task_description` (optional): What the assistant was asked to do, ideally the original prompt or ticket, so the review can check scope.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Code from an AI assistant fails differently from code a colleague wrote. It compiles and reads fluently, so reviewers skim it, but it often calls functions or options that do not exist in the installed library version, adds layers and configuration nobody asked for, catches and discards errors so the happy path "works", edits or deletes tests until they pass, and repeats a pattern across files with small inconsistencies. It also changes files outside the task. This review looks for those failure modes specifically, on top of normal correctness.
</context>

<task>
Review this change:
<diff>
$diff
</diff>
Only if task_description was provided: 
The assistant was asked to:
<task_description>
$task_description
</task_description>

Check, in this order:
1. **Scope.** Compare the files and behaviour changed with the task. List changes the task did not call for (renames, reformatting, new dependencies, unrelated refactors, edited config). If no task description was given, say scope could not be checked.
2. **Hallucinated or misused APIs.** For every imported symbol, method, option, flag, environment variable and config key that the diff introduces, check that it exists in the code base or in the dependency version the project pins. If you can read the repository, look in lockfiles, vendored types or the dependency source. If you cannot verify one, list it as "unverified" rather than calling it wrong.
3. **Tests.** Flag deleted or skipped tests, loosened assertions (exact value replaced by "not null", snapshot regenerated wholesale), mocks that replace the unit under test, tests that assert the implementation instead of the behaviour, and special cases in production code that only exist to satisfy a test.
4. **Error handling.** Flag catch-all handlers that log and continue, empty catch blocks, default values that hide failures, retries without limits, and errors converted to success responses.
5. **Over-engineering.** Flag abstractions with one implementation, factories, strategy patterns and options objects for a single call site, speculative configuration, and new dependencies for a few lines of standard library code. Propose the simpler shape.
6. **Copy-paste drift.** Where similar blocks appear more than once, compare them line by line and flag the ones that differ in ways that look accidental (a different field name, a missing await, an off-by-one in one copy).
7. **Normal correctness and security** issues you find along the way: trace the input that triggers each one.
</task>

<constraints>
- Every finding cites `path:line` and names the concrete failure or cost. Drop anything you cannot tie to a line.
- Do not object to code just because an AI wrote it, and do not comment on formatting or naming unless it causes a defect.
- Report at most 12 findings, ranked by severity: blocker, major, minor.
- Mark each API finding "confirmed missing", "wrong signature" or "unverified", and say how you checked.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: approve | approve-with-changes | request-changes, and the single most important reason.
## Findings
A table: severity, `path:line`, category (scope, api, tests, errors, over-engineering, drift, correctness, security), the problem, the fix.
## Scope check
Bullets of out-of-scope changes to revert or split out, or "Within scope" or "Not checked: no task description".
## Questions for the author
Up to 5 questions the human who ran the assistant must answer before merge.
</output_format>
