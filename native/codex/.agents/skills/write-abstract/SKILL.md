---
name: write-abstract
description: Writes a structured or unstructured abstract within a word limit from a manuscript, keeping every number faithful to the source and showing where each appears. Use before submission.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/write-abstract
  catalog: 2026.1004.0
---

# Write a paper abstract

## Inputs

- [MANUSCRIPT] (required): The manuscript text, or at least its methods and results sections with the main tables.
- [WORD_LIMIT] (optional; default: 250): Maximum number of words in the abstract.
- [STRUCTURE] (optional; one of: structured, unstructured; default: structured): Structured abstracts use labelled sections (Background, Methods, Results, Conclusions); unstructured ones are one paragraph.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
The abstract is the only part of a paper most readers, indexers and reviewers read, so it must stand alone and be exact. Common errors are numbers that differ from the results section, conclusions stronger than the data, a missing primary outcome, undefined abbreviations and going over the limit. Reporting guidelines (for example CONSORT for trials, STROBE for observational studies, PRISMA for systematic reviews) each have abstract checklists, and journals often name the headings they require.
</context>

<task>
Write a [STRUCTURE] abstract of at most [WORD_LIMIT] words from this manuscript:
<manuscript>
[MANUSCRIPT]
</manuscript>

1. Identify the study type, the objective, the design, setting and participants, the primary outcome and its main result, the key secondary results and the authors' conclusion.
2. If the manuscript names a reporting guideline or a target journal's required headings, follow them; otherwise use Background, Methods, Results and Conclusions for a structured abstract.
3. In Results, lead with the primary outcome, giving the effect size with its confidence interval (and p-value if the manuscript reports one) and the number analysed.
4. Write a conclusion that says only what the results support, with the main limitation if it changes how the result should be read.
5. Count the words and cut until you are within the limit: remove background before results, and secondary results before the primary one.
</task>

<constraints>
- Copy every number, unit and interval exactly as it appears in the manuscript. Never round, recompute or combine numbers. If the results section and a table disagree, use neither, flag the conflict in Notes and leave a placeholder such as "[CHECK: n analysed]".
- Include nothing that is not in the manuscript: no new claims, no citations, no references to figures or tables.
- Define each abbreviation at first use, and use at most three abbreviations.
- Match the strength of language to the design: observational studies report associations, not effects.
- If the manuscript has no results (for example only an introduction), say so and ask for the results instead of drafting them.
</constraints>

<output_format>
## Abstract
The abstract, with bold section labels if structured. Then the line "Word count: N / [WORD_LIMIT]".
## Number check
A table: number in the abstract | where it appears in the manuscript (section, table or quoted phrase).
## Notes
Any conflicts, placeholders, or content cut to fit the limit. "None" if clean.
</output_format>
