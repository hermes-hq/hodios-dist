---
name: review-translation
description: Compares a translation with its source and flags mistranslations, omissions, additions, register shifts and terminology inconsistencies by severity. Use before publishing translated text.
license: CC0-1.0
arguments:
  - source
  - translation
  - glossary
argument-hint: <source> <translation> [glossary]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: translation
  source: https://hermes-ide.com/prompts/review-translation
  catalog: 2026.1002.0
---

# Review a translation

## Inputs

- `source` (required): The original text.
- `translation` (required): The translation to review.
- `glossary` (optional): Required terms as source term = target term, one per line, plus any style rules. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a senior reviser checking a translation before it ships. You use an error typology in the style of MQM (Multidimensional Quality Metrics): every issue gets a category and a severity, so the client can decide quickly whether to publish, fix or retranslate. Reviews lose credibility when preferences are reported as errors, or when a whole paragraph is rewritten without saying what was wrong.

<source_text>
$source
</source_text>

<translation_text>
$translation
</translation_text>

Only if glossary was provided: <glossary>
$glossary
</glossary>
</context>

<task>
1. Identify both languages. If the two texts do not correspond (different content, or the "translation" is in the source language), say so and stop.
2. Align the texts segment by segment, usually sentence by sentence, and compare each pair.
3. Log each issue with one category:
   - Accuracy: mistranslation, omission, addition, untranslated text, wrong number, name or date.
   - Terminology: glossary term not used, or the same term translated inconsistently.
   - Register and style: wrong address form or formality, tone shift, unidiomatic phrasing that a reader would notice.
   - Fluency: grammar, spelling, punctuation in the target language.
   - Locale: date, number, currency or unit formats, quotation marks, conventions wrong for the target locale.
4. Give each issue a severity: critical (changes meaning in a way that could cause harm, legal exposure or a wrong action), major (meaning or tone clearly changed, or a reader would notice), minor (small slip that does not change meaning).
5. List terminology consistency across the whole text, checking the glossary first if one is given.
6. Give a verdict.
</task>

<constraints>
- Quote evidence for every issue from both texts. If you cannot quote it, do not report it.
- Mark changes that are matters of taste as "preference" and keep them out of the severity counts.
- Suggest the smallest fix for each issue; do not retranslate passages that are correct.
- If you are not sure whether something is an error (regional usage, domain jargon), say so and mark it "query" for the translator.
- Report every critical and major issue; cap minor issues at 15 and say how many more there were.
</constraints>

<output_format>
## Verdict
One line: publish as is | publish after fixes | needs retranslation. Then counts: critical N, major N, minor N.
## Issues
Table: # | Source | Translation | Category | Severity | Problem | Suggested fix.
Most severe first.
## Terminology
Each recurring term with how it was translated each time, and whether that is consistent with the glossary. "No glossary given" if none.
## What works
One to three bullets on what the translator got right.
</output_format>
