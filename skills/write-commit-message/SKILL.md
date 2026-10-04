---
name: write-commit-message
description: Writes a commit message that states what changed and why, in the repo's own convention, and flags staged changes that should be split. Use before committing.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: git
  source: https://hermes-ide.com/prompts/write-commit-message
  catalog: 2026.1004.3
---

# Write a commit message

## Inputs

- [CHANGES] (optional): The diff or a description of the change. Leave empty to use the staged changes.
- [CONVENTION] (optional; one of: match-repo, conventional, plain; default: match-repo): Message convention to follow.
- [WHY] (optional): The reason for the change, a ticket id or anything the diff cannot show.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A commit message is read months later by someone running `git log`, `git blame` or `git bisect` who needs to know why a line exists. The subject says what changed in words a reader can scan; the body says why, because the diff already shows how. A message that narrates the diff, or one that bundles unrelated changes behind "and", fails that reader.
</context>

<task>
Write a commit message for this change:
Only if [CHANGES] was provided: 
[CHANGES]
If no change is given above, read the staged changes (`git diff --staged`). If nothing is staged, say so in one line and stop.
Only if [WHY] was provided: 
Reason given by the author: [WHY]

1. Read the whole diff and name its single purpose in one sentence. If the diff mixes unrelated purposes (a fix plus a refactor, two features), do not write one message. Propose a split instead: list each commit with its files or hunks and its subject line.
2. Pick the convention: [CONVENTION].
   - `match-repo`: read the last 20 subjects (`git log --format=%s -20`) and copy their pattern: type prefixes, scopes, capitalisation, ticket references. If there is no history or no clear pattern, use `plain`.
   - `conventional`: Conventional Commits 1.0.0. `type(scope): description`, with type one of feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert. Use the scope only if the repo has clear modules. Mark a breaking change with an exclamation mark before the colon (`feat(api)!: ...`) and a `BREAKING CHANGE:` footer that says what users must do.
   - `plain`: a capitalised imperative subject with no prefix.
3. Subject: imperative mood ("Fix", not "Fixed" or "Fixes"), names the thing that changed, no trailing period, at most 72 characters and ideally under 50.
4. Body, after one blank line, wrapped at 72 characters: the problem, why this approach, and any side effect or follow-up a reviewer must know. Skip the body when the subject says everything (typo fixes, version bumps).
5. Footers only for facts you have: issue references from the input, `BREAKING CHANGE:`, or trailers the repo already uses.
</task>

<constraints>
- Never invent a reason, ticket number, issue link, benchmark or test result. If the motivation is not in the diff or the input, write a body with only what the diff proves and add one line after the message asking for the reason.
- Do not add tool or assistant attribution trailers (such as `Co-authored-by`) unless the author asks.
- Do not run `git commit` or change the index. Output the message only.
- Describe behaviour, not files: "Reject expired tokens at login" beats "Update auth.ts".
</constraints>

<output_format>
The message inside one fenced `text` block, exactly as it should be committed.
After the block, at most two lines starting with `Note:` for a proposed split or missing information. Nothing else.
For a split, output one fenced block per proposed commit, each preceded by the files or hunks it contains.
</output_format>

<examples>
Input: a diff that changes `retry.ts` so that `fetchWithRetry` stops retrying on HTTP 4xx responses, with a new test.

```text
Stop retrying client errors in fetchWithRetry

A 4xx response means the request itself is wrong, so retrying it only
adds latency and load: a bad token was retried 5 times per call before
failing. Retry only network errors and 5xx responses, and add a test
that a 401 fails on the first attempt.
```
</examples>
