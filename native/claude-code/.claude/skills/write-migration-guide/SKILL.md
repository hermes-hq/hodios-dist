---
name: write-migration-guide
description: Writes an upgrade guide for a breaking release that lists each breaking change with how to find affected code, before-and-after examples and a way to verify. Use when shipping a major version.
license: CC0-1.0
arguments:
  - from_version
  - to_version
  - changes
argument-hint: <from_version> <to_version> [changes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: docs
  source: https://hermes-ide.com/prompts/write-migration-guide
  catalog: 2026.1004.0
---

# Write a migration guide

## Inputs

- `from_version` (required): The version users are upgrading from (tag or version number).
- `to_version` (required): The version users are upgrading to.
- `changes` (optional): Changelog, release notes or a list of breaking changes, if you have them. The guide still checks them against the code.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A migration guide is used by someone who has to upgrade without breaking production. They need to know whether they are affected, how to find the affected code in their own codebase, exactly what to change, and how to confirm it worked. A changelog line like "Renamed `connect` options" is not enough: the reader needs the old and new code side by side.
</context>

<task>
Write the guide for upgrading from $from_version to $to_version.
Only if changes was provided: 
Known changes:
$changes

1. Build the list of breaking changes from the changelog, release notes, commits marked breaking (an exclamation mark before the colon in the header, or a `BREAKING CHANGE` footer) and a diff of the public surface between the two versions: exported symbols, function signatures, CLI flags, config keys, environment variables, defaults, HTTP routes and response shapes, minimum runtime versions and peer dependencies.
2. Check each change against the code at both versions. Drop anything that is not actually breaking for users; add breaking changes the notes missed.
3. For each breaking change write: what changed and why (one or two sentences), who is affected and how to find affected code (a search pattern or symptom such as an error message), a before and after code example, and the exact steps. If a mechanical rewrite is safe, give it, and say when it is not safe.
4. Order changes by how many users they affect, most common first. Group small related changes.
5. List deprecations that still work but will break in a later version, with the replacement.
6. End with how to verify: commands, tests or observable behaviour that confirm the upgrade worked, and how to roll back.
</task>

<constraints>
- Every claimed change must be traceable to the code, the commits or the given notes. Mark anything you inferred but could not confirm with `TODO(maintainer): ...`.
- Before and after examples must use real names and signatures from the two versions. Never invent options or APIs.
- Do not soften breaking changes or hide them in prose; one heading per change.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
# Upgrading from $from_version to $to_version
## Who needs this
Two or three sentences, including the effort level (minutes, hours) if it can be judged.
## Before you start
Prerequisites: runtime versions, peer dependencies, a backup or a database migration.
## Breaking changes
One `###` heading per change, each with: what changed, how to find affected code, Before and After code blocks, steps.
## Deprecations
A table: deprecated | replacement | removal planned in. Or "None".
## Verify the upgrade
Numbered checks, then rollback steps.
</output_format>
