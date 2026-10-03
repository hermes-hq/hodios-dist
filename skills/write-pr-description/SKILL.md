---
name: write-pr-description
description: Writes a pull request description that tells reviewers why the change exists, what to look at first, how to test it and what could break. Use when opening a PR.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: git
  source: https://hermes-ide.com/prompts/write-pr-description
  catalog: 2026.1003.0
---

# Write a pull request description

## Inputs

- [CHANGES] (optional): Diff, branch name or commit range. Leave empty to compare the current branch with the default branch.
- [WHY] (optional): The ticket, issue or reason for the change, if the diff does not show it.
- [TEMPLATE] (optional): The repo's PR template, if it is not in the repo. Its headings replace the default ones.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A PR description is for the reviewer, who has less context than the author and limited time. A good one answers, in order: what does this do, why now, where should I look first, how do I know it works, and what could go wrong. It is not a changelog of every file and not a sales pitch. Its length should follow the size and risk of the change: two lines for a typo fix, a full page for a migration.
</context>

<task>
Write the description for Only if [CHANGES] was provided: [CHANGES]. If no change is given, diff the current branch against the default branch (`git merge-base` with `origin/HEAD`, then `git diff` and `git log` from there).
Only if [WHY] was provided: 
Reason given by the author: [WHY]
Only if [TEMPLATE] was provided: 
Use the headings of this template instead of the default ones, and fill every section it has:
[TEMPLATE]

1. Read every commit message and the full diff before writing. Check the repo for a PR template (`.github/pull_request_template.md`, `.github/PULL_REQUEST_TEMPLATE/`, `docs/`) and use it if one exists.
2. State the purpose in one or two sentences a reviewer could repeat.
3. Group the changes by intent, not by file. Point to the one or two places that carry the risk ("start with `billing/proration.ts`; the rest is wiring").
4. Write test steps a reviewer can follow: commands, inputs and expected results. Include only tests and checks you can see in the diff or the input.
5. List what could break: behaviour changes, migrations, config or environment changes, feature flags, performance, and how to roll back.
</task>

<constraints>
- Never claim that tests pass, that something was tested manually, or that metrics improved unless the input says so. Write `TODO(author): ...` for anything only the author can confirm.
- Link issues only when the id appears in the branch name, commits or input. Never invent one.
- Call out breaking changes and required deploy steps (migrations, new env vars) at the top of Risks, in bold.
- No filler ("This PR aims to..."), no restating the title, no emoji unless the template uses them.
- Do not create or edit the PR yourself; output the text.
</constraints>

<output_format>
First line: a proposed PR title in the repo's commit style, under 72 characters.
Then, unless a template replaces them, these sections, omitting any that would be empty for a small change:
## Summary
One or two sentences.
## Why
The problem or ticket, with the link if known.
## Changes
Bullets grouped by intent. Name the files to review first.
## How to test
Numbered steps with expected results.
## Risks
Breaking changes, migrations, rollout and rollback, or "Low: ..." with the reason.
</output_format>
