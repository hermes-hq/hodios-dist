---
name: write-acceptance-criteria
description: Writes testable acceptance criteria for a user story or ticket, covering the main path, alternatives, validation, boundaries, permissions and empty states. Use before a story enters development.
license: CC0-1.0
arguments:
  - story
  - context
  - criteria_style
argument-hint: <story> [context] [criteria_style]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product
  source: https://hermes-ide.com/prompts/write-acceptance-criteria
  catalog: 2026.1002.1
---

# Write acceptance criteria

## Inputs

- `story` (required): The user story or ticket text.
- `context` (optional): Business rules, limits, roles and screens that apply.
- `criteria_style` (optional; one of: gherkin, checklist; default: gherkin): gherkin gives Given/When/Then scenarios; checklist gives short verifiable statements.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Acceptance criteria are the shared definition of done between product, engineering and testing. Good criteria describe observable behaviour with concrete values, so two people reading them would test the same thing. Most production bugs in new features sit in the cases the criteria never mentioned: boundaries, permissions, errors and empty states.
</context>

<task>
Write acceptance criteria for this story: $story
Only if context was provided: 
Rules and context that apply:
$context
Style: $criteria_style.

1. Identify the main path and write it first.
2. Add the cases that apply to this story: alternative paths, input validation, exact boundaries (at, just below and just above each limit), permissions for each role, empty and first-use states, errors from dependencies, and repeated or concurrent actions.
3. Use concrete example values in every criterion (amounts, dates, names, counts), not "valid input".
4. Check every criterion: could a tester verify it with no further explanation? Rewrite any that fail.
</task>

<constraints>
- Describe behaviour the user or a system can observe, not implementation or UI layout, unless the story is about the layout.
- Each scenario stands alone and tests one behaviour.
- At most 12 criteria. If the story needs more, say that it should be split and suggest where.
- Do not invent business rules. If a criterion needs a rule that was not given, write it with your best guess, mark it "Assumption:", and repeat it under Questions for the product owner.
</constraints>

<output_format>
## Acceptance criteria
For gherkin: numbered scenarios, each with a `Scenario:` title and Given, When, Then lines (And where needed).
For checklist: numbered "- [ ]" items, one verifiable statement each.
## Assumptions
Bullets, or "None".
## Questions for the product owner
Numbered, or "None".
</output_format>
