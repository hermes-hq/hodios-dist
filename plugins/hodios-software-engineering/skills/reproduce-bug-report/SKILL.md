---
name: reproduce-bug-report
description: Turns a vague bug report into a minimal, reliable reproduction, preferably a failing test, and states the exact conditions needed. Use before fixing a reported bug or when triaging issues.
license: CC0-1.0
arguments:
  - report
  - environment
argument-hint: <report> [environment]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: debugging
  source: https://hermes-ide.com/prompts/reproduce-bug-report
  catalog: 2026.1003.2
---

# Turn a bug report into a minimal reproduction

## Inputs

- `report` (required): The bug report or issue text, with any screenshots described, logs and version information.
- `environment` (optional): Where the reporter saw it, for example version, OS, browser or configuration, if the report does not say.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A bug that cannot be reproduced cannot be fixed with confidence. Reports mix what the user saw with what they think caused it, and they leave out the conditions that matter. A minimal reproduction strips everything that is not needed to trigger the failure, which often points straight at the cause.
</context>

<task>
Reproduce this report:
$report
Only if environment was provided: 
Environment: $environment
1. Separate the report into observations (what the user saw) and interpretations (what they think caused it). Work from the observations.
2. Write down the expected and the actual behaviour in one line each. If the report does not make expected behaviour clear, say so.
3. Reproduce it in the codebase, starting at the closest level you can: a unit or integration test first, then a script or command, and manual steps only as a last resort.
4. Minimise: remove inputs, steps and configuration one at a time while the failure still happens. Then vary the conditions that seem to matter (data shape, version, platform, timing, configuration) to find which ones are required.
5. Leave the reproduction in place as a failing test, marked so it is easy to find, or as exact steps if a test is not possible.
</task>

<constraints>
- Do not fix the bug. This task ends at a reliable reproduction.
- If you cannot reproduce it, do not pretend you did. List the attempts and the conditions you tried, and write the questions for the reporter that would unblock you.
- Keep the reproduction free of real user data. Use synthetic values with the same shape.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Status
`reproduced`, `partly reproduced` or `not reproduced`, and the failure rate when it is intermittent.
## Reproduction
The failing test (path and code) or the exact steps and command, and its output.
## Conditions
Bullets: what must be true for the failure to happen, and what turned out not to matter.
## Expected and actual
Two lines.
## Unknowns
Questions for the reporter, or "None".
</output_format>
