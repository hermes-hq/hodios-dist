---
name: improve-naming
description: Proposes clearer names for variables, functions, types and modules, explains each rename and applies them without changing behaviour. Use when code reads poorly because of its names.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/improve-naming
  catalog: 2026.1003.2
---

# Improve naming in code

## Inputs

- [CODE] (required): The code to improve, pasted, or file paths in the repo.
- [DOMAIN_GLOSSARY] (optional): The business terms the team uses and what they mean, for example "a Booking is confirmed; a Reservation is only held".
- [CONVENTIONS] (optional): Naming conventions to follow, for example "PEP 8", "Go: short receiver names, no Get prefix", or a link to the style guide. Leave empty to follow the language's and the codebase's conventions.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Names are most of what a reader has to understand code. Bad names come in recognisable kinds: vague (`data`, `info`, `handle`, `process`, `Manager`), misleading (`getUser` that also creates one, `isValid` that returns a list of errors), inconsistent (`customer`, `client` and `account` for the same thing), encoded (`strName`, `arrItems`), wrong in scope (one-letter names that live for 80 lines, or long names for a two-line loop index), and out of step with the business language. A rename is only an improvement if the new name is more accurate, consistent with the codebase and the domain, and applied everywhere without changing behaviour.
</context>

<task>
Improve the names in:

<code>
[CODE]
</code>

Only if [DOMAIN_GLOSSARY] was provided: 
Domain glossary:
[DOMAIN_GLOSSARY]
Only if [CONVENTIONS] was provided: 
Conventions: [CONVENTIONS]

1. Read the code and enough of its callers to understand what each name really refers to and does. For functions, check what they actually do, including side effects and return values, not what their name claims.
2. Find names worth changing and classify each: vague, misleading, inconsistent with the rest of the codebase or the glossary, encoded type or scope, wrong length for its scope, or a convention violation (case, prefixes, verb tense for booleans and functions).
3. For each, propose one name following these rules: use the glossary's terms; functions are verbs that say what they do and reveal side effects (`loadOrCreateUser`, not `getUser`); booleans read as yes or no questions (`isExpired`, `hasAccess`); collections are plural; units go in the name when the type does not carry them (`timeoutMs`); length grows with scope; match the existing codebase's conventions over personal preference. If a name is misleading because the function does two things, say so and suggest the split in one line instead of hiding it with a longer name.
4. Separate safe renames from risky ones. Risky renames include public API, exported symbols used by other packages, serialised field names (JSON, database columns, message schemas), configuration keys, names used via reflection, string-based lookups, templates or dependency injection, and anything in a published SDK. Do not apply risky renames; list them with the migration they would need.
5. Apply the safe renames everywhere they are referenced, using the language's refactoring tooling or a careful search that also covers tests, comments and docs in the repo. If the code was pasted rather than in a repo, return the rewritten code.
6. Run the type checker, linter and tests if they exist, and report the real results. Behaviour must not change.
</task>

<constraints>
- Change names only. No logic changes, no reformatting, no reordering, no new abstractions.
- Do not rename for taste: every rename has a reason from step 2. If the existing name is fine, leave it.
- Keep the number of renames proportionate; prefer the 5 to 15 that most improve understanding over renaming everything.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Rename table
Table: old name, new name, kind (variable, function, type, module), problem, why the new name is better. Applied renames only.
## Not renamed
Table: name, proposed name, why it was not applied (public API, serialised, reflection) and the migration it would need. Or "None".
## Changes
For pasted code, the full rewritten code in one fenced block. For a repo, one line per file changed.
## Verification
The checks run and their real results, or which checks could not be run.
</output_format>
