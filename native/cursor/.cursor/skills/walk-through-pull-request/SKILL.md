---
name: walk-through-pull-request
description: Explains a large or unfamiliar pull request to its reviewer with what changes and why, a reading order, the risky hunks and questions for the author. Use before reviewing a big diff.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: code-review
  source: https://hermes-ide.com/prompts/walk-through-pull-request
  catalog: 2026.1003.1
---

# Walk a reviewer through a pull request

## Inputs

- [DIFF] (required): The unified diff, a PR URL or a branch name.
- [PR_DESCRIPTION] (optional): The PR description and linked ticket or design doc, if any.
- [REVIEWER_FAMILIARITY] (optional; one of: new, some, owner; default: some): How well the reviewer knows this code. new needs the surrounding concepts explained; owner wants only what changed and the risks.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Faced with a 2,000-line diff in alphabetical file order, reviewers skim, approve the parts they understand and miss the hunk that matters. The fix is not a second reviewer but a guide: what the change is trying to do, which files carry the idea and which are mechanical fallout, the order that makes the diff read like a story, and where a careful reviewer should slow down. This prompt prepares the reviewer; it does not do the review or pass a verdict.
</context>

<task>
Prepare a reviewer to review this change. The reviewer's familiarity with the code is: [REVIEWER_FAMILIARITY].

<diff>
[DIFF]
</diff>

Only if [PR_DESCRIPTION] was provided: 
<pr_description>
[PR_DESCRIPTION]
</pr_description>

1. If [DIFF] is a URL or branch name, fetch the diff and the PR description with the tools you have. If you cannot, ask for the diff once and stop.
2. Read the whole diff before writing anything. Where the repo is available, read the surrounding code of the main changed functions so your explanation is right about what the code did before.
3. Work out the intent: what problem the change solves and how, in terms of behaviour. If the PR description and the diff disagree, say so.
4. Group the changed files into: core logic (where the idea lives), interfaces and contracts (APIs, schemas, public types, config), data changes (migrations, backfills), tests, and mechanical changes (renames, moves, generated code, formatting, dependency bumps). Give approximate line counts per group so the reviewer knows where the real reading is.
5. Propose a reading order that builds understanding: usually contracts and data shapes first, then the core logic in call order, then the callers, then tests, with mechanical changes last or skipped. Give one line per stop saying what to look for there.
6. Point out the risky hunks with `path:line` references: behaviour changes hidden in refactors, changed defaults, concurrency, error handling, migrations and backwards compatibility, security-sensitive code, and anything with no test. Say why each deserves attention; do not claim a bug unless you can name the input that triggers it.
7. Write questions for the author that a reviewer would need answered to approve: missing context, unexplained decisions, rollout and rollback, test coverage gaps.
8. Adjust depth to familiarity: for new, explain the domain terms, the modules involved and how a request flows through them before the reading order; for some, explain only the parts of the system this change touches; for owner, skip background and focus on the diff and its risks.
</task>

<constraints>
- Do not approve, reject or give a verdict. The reviewer decides.
- Describe what the code does, not what the author probably meant, and mark any inference about intent as an inference.
- Every claim about a hunk cites `path:line` or a function name from the diff.
- If the diff is too large to read fully in one pass, say which parts you read closely and which you only skimmed.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## In one paragraph
What the change does, why, and how big it really is once mechanical changes are excluded.
## What changes
Table: group, files, approximate lines, what changes in behaviour.
## Reading order
Numbered stops: `path` (or function), what to look for.
## Risky hunks
Numbered: `path:line`, what is risky and why, what to check.
## Questions for the author
Numbered.
## Not covered
What you did not read closely or could not verify, or "Nothing".
</output_format>
