---
name: self-review-before-pr
description: Reviews your own branch the way a strict reviewer would, catches debug leftovers, unrelated changes, missing tests and leaked secrets, and runs the checks. Use before requesting review.
license: CC0-1.0
arguments:
  - base
  - checks
argument-hint: "[base] [checks]"
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: code-review
  source: https://hermes-ide.com/prompts/self-review-before-pr
  catalog: 2026.1003.2
---

# Self-review a branch before opening a PR

## Inputs

- `base` (optional; default: main): Branch or commit the work will merge into.
- `checks` (optional): Commands that must pass, for example "npm test && npm run lint". If empty, use what the project's README, CI config or task runner defines.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Reviewers spend most of their time on problems the author could have caught alone: a forgotten debug print, a file changed by accident, a test that was never run. A self-review pass before asking for review shortens the review and keeps the reviewer's attention on design and correctness.
</context>

<task>
Review the changes on the current branch compared with $base.
1. Get the diff with `git diff $base...HEAD` and the commit list with `git log $base..HEAD`. Also check `git status` for uncommitted or untracked files that look like they belong in the change.
2. Read the whole diff and write one sentence describing what the change does. Every hunk should serve that sentence.
3. Look for:
   - Leftovers: debug prints, commented-out code, `TODO` or `FIXME` added in this branch, temporary files, focused or skipped tests (`.only`, `xit`, `@Ignore`, `t.Skip`).
   - Unrelated changes: reformatting, renames or edits outside the purpose of the change.
   - Secrets and personal data: keys, tokens, passwords, internal hostnames, real customer data in fixtures.
   - Missing tests: changed behaviour with no test that would fail without the change.
   - Defects you can see: unhandled errors, wrong conditions, null or empty inputs, resource leaks.
   - Generated or lock files changed without the source change that explains them.
4. Run the checks and report the real result of each. Only if checks was provided: Run exactly these: $checks If no commands are listed in this step, run the test, lint and type-check commands the project defines (look in the README, CI config, package scripts, Makefile or equivalent).
</task>

<constraints>
- Report, do not edit. The author decides what to change.
- Cite `path:line` for every finding.
- Separate blockers (would fail review or break something) from cleanups (worth fixing, not blocking).
- If you find what looks like a real secret, say which file and line, and tell the author to rotate it. Do not repeat the secret value.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Ready
`yes` or `no`, then one sentence.
## Blockers
Numbered: `path:line`, the problem, the fix. Or "None".
## Cleanups
Bullets: `path:line` and what to clean. Or "None".
## Checks
Each command, `pass` or `fail`, and the first relevant error line for failures. Say plainly if a check could not run.
## Notes for the reviewer
Two or three bullets: what the change does, where to look first, anything deliberately left out.
</output_format>
