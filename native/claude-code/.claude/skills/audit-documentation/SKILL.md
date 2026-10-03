---
name: audit-documentation
description: Audits documentation for accuracy against the code, gaps in the user journey, stale pages, duplication and findability, and returns a prioritised fix list. Use before a docs overhaul or release.
license: CC0-1.0
arguments:
  - docs
  - code_or_changelog
  - audience
argument-hint: <docs> [code_or_changelog] [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: docs
  source: https://hermes-ide.com/prompts/audit-documentation
  catalog: 2026.1003.2
---

# Audit a documentation set

## Inputs

- `docs` (required): The documentation to audit, pasted, as a folder in the repo, or as a list of pages with their content.
- `code_or_changelog` (optional): The code, public API, CLI help output or changelog to check the docs against.
- `audience` (optional): Who the docs are for, for example "developers integrating our REST API", "self-hosting operators", "end users".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Documentation decays quietly. Options get renamed in the code but not in the docs, examples stop compiling, the getting-started page assumes a step that was removed two releases ago, three pages explain the same concept differently, and the page people need exists but nobody can find it. An audit is useful only if its findings are specific (which page, which line, what is wrong, what is true instead), checked against the source of truth rather than guessed, and ranked by how much they hurt readers, so the team can fix the worst things first.
</context>

<task>
Audit this documentationOnly if audience was provided:  for $audience.

<docs>
$docs
</docs>

Only if code_or_changelog was provided: 
Source of truth to check against:
<code_or_changelog>
$code_or_changelog
</code_or_changelog>

1. Inventory the pages: title, apparent purpose, and type using the Diátaxis categories (tutorial, how-to guide, reference, explanation). Note pages that mix types in a way that confuses readers.
2. **Accuracy.** Check every verifiable claim against the source of truth (or the repo, if you can read it): command names and flags, configuration keys and defaults, function and endpoint signatures, response fields, environment variables, version numbers and supported platforms, and code examples (do they use APIs that exist with the right arguments?). Record each mismatch with what the docs say and what the code says. If there is no source of truth for an area, say it was not checked.
3. **Journey gaps.** Walk the main reader journeys for the audience: evaluate, install, first success, common tasks, configuration, troubleshooting, upgrade and reference lookup. For each, note missing steps, missing pages, assumed knowledge, dead ends and places where the reader has to leave the docs.
4. **Stale and duplicate pages.** Flag pages that describe removed or deprecated behaviour, refer to old versions, or have no clear owner; and pages that duplicate or contradict each other, naming which one should be the canonical page.
5. **Findability.** Assess navigation and titles: can a reader find each journey's pages from the landing page in a few clicks, do titles use the words readers would search for (error messages, task names), are there orphan pages, broken or circular links, and missing cross-links between related pages.
6. Prioritise every finding by reader impact (how many readers hit it and how badly: wrong instructions that break things rank highest, cosmetic issues lowest) and by effort, and produce a fix list.
</task>

<constraints>
- Every finding cites the page (and heading or line where possible) and, for accuracy issues, the evidence from the code or changelog. No vague findings such as "improve clarity".
- Do not claim something is wrong unless you checked it against a source; mark suspected issues as "suspected" with what would confirm them.
- Do not rewrite the docs in this pass. Suggested fixes are one or two sentences each.
- Ignore pure style preferences unless they affect understanding.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Summary
Five lines at most: overall state, the three most damaging problems, and what was not checked.
## Accuracy
Table: page and location, docs say, code says, severity.
## Journey gaps
Per journey: what is missing or broken.
## Stale and duplicate pages
Table: page, problem, canonical page or action.
## Findability
Bullets.
## Prioritised fix list
Table: priority (P1 to P3), fix, pages, effort (S, M, L), why it matters.
## Not checked
What you could not verify and what you would need.
</output_format>
