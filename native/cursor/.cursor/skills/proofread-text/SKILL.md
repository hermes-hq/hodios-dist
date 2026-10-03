---
name: proofread-text
description: Corrects grammar, spelling, punctuation and consistency errors in the chosen English variety, preserving the author's voice, and lists each change with the rule behind it.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: editing
  source: https://hermes-ide.com/prompts/proofread-text
  catalog: 2026.1003.0
---

# Proofread a text

## Inputs

- [TEXT] (required): The text to proofread.
- [VARIANT] (optional; one of: us, uk, au, ca; default: us): English spelling and punctuation variety.
- [STYLE_GUIDE] (optional): Optional house or published style guide to follow, for example "AP", "Chicago", "New Hart's Rules" or a few house rules.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Proofreading is the last pass: it fixes errors, not style. Authors stop trusting a proofreader who rewrites sentences they liked, "corrects" a deliberate fragment, or silently changes British spelling to American. They also need to see every change, because a wrong correction in a contract, a name or a number is worse than the original typo.

Variety notes: US uses -ize, -or, -er (center), single quotation marks only inside double. UK commonly uses -ise (Oxford style keeps -ize), -our, -re, and single quotation marks first. Australian follows British spelling with -ise. Canadian uses -our and -re (colour, centre) with -ize (organize), and "cheque".
</context>

<task>
Proofread the text below in [VARIANT] English.Only if [STYLE_GUIDE] was provided:  Follow this style guide where it applies: [STYLE_GUIDE].

<text>
[TEXT]
</text>

1. If the text is empty, ask for it and stop.
2. Fix objective errors: spelling and typos, doubled or missing words, subject-verb agreement, tense slips, pronoun reference errors, wrong word (affect/effect, its/it's), punctuation errors (comma splices, missing closing quotes or brackets, misplaced apostrophes), and capitalisation errors.
3. Fix spelling that does not match [VARIANT] English, except in quotations, proper nouns and titles.
4. Enforce internal consistency where the text varies: serial comma, number style, hyphenation of compounds, capitalisation of terms, date format, abbreviations. Follow the style guide if given; otherwise follow the form the text uses most.
5. Leave style alone: sentence length, word choice that is correct, deliberate fragments, informal register, starting a sentence with "And" or "But", splitting infinitives, ending with a preposition.
6. Do not change names, numbers, figures, legal or technical terms, code, URLs or quoted material. If one looks wrong, raise it as a query.
</task>

<constraints>
- Every change in the corrected text appears in the Changes table, and nothing changes that is not listed.
- Name the actual rule for each change, not "improved flow".
- When a usage is disputed or depends on the style guide (for example "data is" or "data are"), leave it and note it under Queries only if it is inconsistent.
- If the text is clean, say so and return it unchanged.
</constraints>

<output_format>
## Corrected text
The full text with corrections applied.
## Changes
A table: # | Original | Corrected | Rule. In order of appearance.
## Queries
Bullets: possible problems you did not change because they need the author's decision (facts, names, numbers, ambiguous meaning, deliberate-looking style). "None" if none.
</output_format>
