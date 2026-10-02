---
name: upgrade-major-dependency
description: Upgrades a library or framework across major versions using the official migration notes, fixes what breaks, and proves the result with before-and-after checks. Use for any breaking upgrade.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: migration
  source: https://hermes-ide.com/prompts/upgrade-major-dependency
  catalog: 2026.1002.1
---

# Upgrade a major dependency

## Inputs

- [DEPENDENCY] (required): The package, library or framework to upgrade, as named in the manifest.
- [TARGET_VERSION] (optional; default: the latest stable release): The version to upgrade to.
- [NOTES] (optional): Known constraints, such as other packages that must stay put or a migration guide you want followed.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Major upgrades fail in two ways: breaking changes that nobody noticed until production, and "fixes" that silence the compiler or the tests instead of adapting the code. Model memory of a library's breaking changes is often out of date, so the upgrade must follow the official release notes, and success must be shown by the same checks passing before and after.
</context>

<task>
Upgrade [DEPENDENCY] to [TARGET_VERSION].
Only if [NOTES] was provided: 
Notes:
[NOTES]

1. Find the current version in the manifest and lockfile, every place the code uses the dependency, and the packages that depend on it or must move with it (plugins, type packages, peer dependencies).
2. Get the official changelog or migration guide for every major version between the current and the target. Fetch it if you can; otherwise ask the user to paste it and stop until they do. Do not rely on memory for the list of breaking changes.
3. Run the project's build, type check, linter and tests before changing anything, and record the results as the baseline. Find the commands in the repo's scripts or docs.
4. Match each breaking change against the code and list the ones that apply, with the affected files.
5. Upgrade with the project's package manager, one major version at a time when several are skipped, together with the packages that must move with it. Use the official codemod when one exists, then review its output.
6. Fix compile errors first, then failing tests, then deprecation warnings that the target version turns into errors.
7. Run the same checks as the baseline and compare.
</task>

<constraints>
- Upgrade only what this upgrade requires. No unrelated version bumps, refactors or formatting.
- Never edit the lockfile by hand; let the package manager write it.
- Do not silence problems: no new `any` casts, ignore comments, disabled lint rules, skipped tests or pinned sub-dependencies to work around a breaking change.
- If a breaking change has no safe equivalent, or a behaviour change needs a product decision, stop and ask.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Summary
One line: from version, to version, and whether all checks pass.
## Breaking changes that applied
Table: change (with a link or reference to the release notes), affected files, how it was fixed.
## Changes made
Bullets, grouped by file or area.
## Verification
Table: check, command, before, after.
## Follow-ups
Deprecations left for later, behaviour changes to watch in production, and anything you could not verify.
</output_format>
