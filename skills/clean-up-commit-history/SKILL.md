---
name: clean-up-commit-history
description: Plans an interactive rebase that turns a messy branch into logical, reviewable commits, with a backup, the exact todo list and a check that the code is unchanged. Use before merging a WIP branch.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: git
  source: https://hermes-ide.com/prompts/clean-up-commit-history
  catalog: 2026.1002.0
---

# Clean up a branch's commit history

## Inputs

- [LOG] (required): Output of `git log --oneline --stat <base>..HEAD` (or similar) for the branch, plus the base branch name.
- [TARGET_SHAPE] (optional): How the history should look, for example "one commit per layer", "refactor first, then feature, then tests", or the team's commit convention.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Reviewers read history commit by commit, and `git bisect` and `git revert` work on commits, so each commit should be one logical change that builds on its own. Work-in-progress history ("wip", "fix typo", "address review") is normal while working and should be reshaped before merge. Interactive rebase is the tool, but it rewrites commits: the risks are losing work, breaking a shared branch, and ending with a final tree that differs from what was tested. A backup and a tree comparison remove those risks.
</context>

<task>
Plan the clean-up of this branch:
[LOG]
Only if [TARGET_SHAPE] was provided: Target shape: [TARGET_SHAPE]

1. Read the log and the files each commit touches. Group the changes into logical commits: one purpose each, ordered so every commit builds and passes tests (refactors and moves before the behaviour that depends on them; tests with the code they test unless the target shape says otherwise). If the log is missing the base branch or file stats, ask for them.
2. Write the target history: the list of final commits with a subject line in the team's convention (imperative mood, under about 72 characters if no convention is given) and which original commits feed each one.
3. Map every original commit to a rebase action: `pick`, `reword`, `squash`, `fixup`, `drop` or `edit` (to split). Reorder lines as needed. Point out where reordering will likely conflict, because a later commit touches the same lines as an earlier one.
4. For commits that mix two purposes, give the split procedure: mark `edit`, `git reset HEAD~`, stage by purpose with `git add -p` or by path, commit each part, then `git rebase --continue`.
5. Mention the fixup alternative for future work: `git commit --fixup=<sha>` plus `git rebase -i --autosquash`.
6. Give the verification: the final tree must equal the backup's tree, and each commit should build and test.
</task>

<constraints>
- The first step is always a backup branch. Never suggest `git reset --hard` or `git push --force` without `--force-with-lease`.
- If the branch is already pushed and others may have based work on it, say so, and recommend agreeing with them before rewriting.
- Never drop a commit whose changes are not present elsewhere in the target history; if a change looks accidental, list it and ask.
- Use only commit hashes and messages from the log. Do not invent commits.
</constraints>

<output_format>
## Target history
Numbered final commits: subject, then the original commits it absorbs.
## Before you start
The backup command (`git branch backup/<branch>-<date>`) and a check that the working tree is clean.
## Rebase todo
The `git rebase -i <base>` command and the full todo list exactly as it should be edited, oldest first.
## Splitting and rewording
Step-by-step commands for each `edit` and the new messages for each `reword` or `squash`.
## Verify
`git diff backup/<branch>-<date> HEAD` must be empty, plus `git rebase -x "<test command>" <base>` to build and test each commit.
## Publish
`git push --force-with-lease` and when it is safe.
## Undo
How to return to the backup (or find the old head in `git reflog`) if anything goes wrong.
</output_format>
