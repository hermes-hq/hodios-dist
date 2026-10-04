---
name: write-release-notes
description: Turns merged pull requests or commits into release notes for a chosen audience, grouped by impact and written as outcomes without internal jargon. Use when shipping a version.
license: CC0-1.0
arguments:
  - changes
  - audience
  - version
argument-hint: <changes> [audience] [version]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: docs
  source: https://hermes-ide.com/prompts/write-release-notes
  catalog: 2026.1004.2
---

# Write release notes

## Inputs

- `changes` (required): Merged PR titles and descriptions, commit messages, or a compare log for the release.
- `audience` (optional; one of: end-users, developers, admins; default: end-users): Who reads the notes. end-users = people using the product; developers = people integrating with an API, SDK or library; admins = people deploying, configuring or operating it.
- `version` (optional): Version number or release name for the heading.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Commit logs describe what engineers did; release notes describe what changed for the reader. Readers scan for three things: does anything break or need action from me, what can I now do that I could not before, and was the problem I reported fixed. Notes that list refactors, ticket numbers and component names bury those answers. Notes that inflate a minor fix or guess at a change's effect mislead people.
</context>

<task>
Write release notesOnly if version was provided:  for $version for $audience from these changes:
$changes

1. Classify every change: breaking or action required, new, improved, fixed, security, deprecated, or internal (no effect the reader can notice).
2. Drop internal changes: refactors, CI, test, tooling and dependency bumps, unless they change behaviour, performance the reader would notice, supported versions, or fix a security issue.
3. Merge changes that are parts of one outcome into a single item.
4. Rewrite each item as one sentence about the outcome for the reader, in their words: "You can now export invoices as PDF" rather than "Add PdfRenderer to InvoiceService". Fixes say what used to go wrong. For developers, name the public API, endpoint, flag or config key affected, and nothing more internal than that. For admins, include configuration, migration, permission, compatibility and deployment impact.
5. Every breaking change or required action gets what breaks, who is affected and the exact step to take, before anything else.
6. When a change's user-facing effect is unclear from the input, do not guess: put it under "Questions".
</task>

<constraints>
- No internal details: no class, file or component names, ticket numbers, author names or architecture terms, except public API names for developers.
- Do not overstate: no "blazing fast", "major overhaul" or invented numbers. Use a performance figure only if the input gives it.
- Keep each item to one sentence. Order sections by impact on the reader, and items within a section by how many readers they affect.
- Omit empty sections.
</constraints>

<output_format>
## Release notes
The notes, ready to paste: a `###` heading with the version if given, an optional one-sentence highlight, then `####` sections in this order: Action required, New, Improved, Fixed, Security, Deprecated. Each item is a bullet.
## Left out
Bullets: each dropped change and why it was left out (internal, merged into another item).
## Questions
Bullets: changes whose user-facing effect you could not determine. Or "None".
</output_format>
