---
name: build-literature-matrix
description: Extracts a comparison matrix across several papers (question, design, sample, findings, limitations) with every cell traceable to its source. Use when organising sources for a literature review.
license: CC0-1.0
arguments:
  - papers
  - columns
argument-hint: <papers> [columns]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: literature-review
  source: https://hermes-ide.com/prompts/build-literature-matrix
  catalog: 2026.1002.1
---

# Build a literature matrix

## Inputs

- `papers` (required): The papers to compare, each with at least a citation and an abstract; full text or your notes give better cells. Separate papers clearly.
- `columns` (optional; default: citation, research question, design, sample and setting, measures, key findings, limitations): Comma-separated columns to extract, if you want something other than the default set.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A literature matrix (also called an evidence or synthesis table) puts every study on the same row structure so the reviewer can compare them and write a thematic synthesis instead of a list of summaries. It is only useful if it is faithful: a cell that paraphrases loosely, fills a gap with a guess or mixes up two papers poisons every later step of the review.
</context>

<task>
Build a matrix from these sources:
<papers>
$papers
</papers>

Columns: $columns

1. Give each paper a short ID (first author + year, adding a/b for duplicates) and use it in every section.
2. Fill one row per paper and one cell per column, using that paper's text only.
3. Keep numbers exactly as written, with units and the comparison they belong to (for example "OR 1.42, 95% CI 1.10-1.83, smokers vs non-smokers").
4. When a value is not stated, write "NR" (not reported). When you derived it rather than read it (for example a design you inferred from the description), add "[inferred]" and keep the inference minimal.
5. After the table, record anything that made extraction uncertain and the patterns a reviewer should check next.
</task>

<constraints>
- Never fill a cell from general knowledge about the paper or its authors. NR is a correct answer.
- Keep each cell under about 25 words; put longer detail in the extraction notes.
- Use the same vocabulary across rows (for example always "RCT", "cohort", "cross-sectional") so the columns can be sorted and compared.
- If the input looks like a single paper, or the papers cannot be told apart, say so and ask how to split them before building the table.
- Patterns are prompts for the reviewer to verify, not conclusions. Do not rank studies as better or worse unless a quality column was requested.
</constraints>

<output_format>
## Matrix
A Markdown table with "ID" as the first column, then the requested columns, one row per paper in chronological order.
## Extraction notes
Bullets: ID, the cell, and what was ambiguous, missing or inferred. "None" if clean.
## Patterns to check
Three to five bullets naming agreements, disagreements or differences in design, population or measures across rows, each citing the IDs involved.
</output_format>
