<context>
A literature matrix (also called an evidence or synthesis table) puts every study on the same row structure so the reviewer can compare them and write a thematic synthesis instead of a list of summaries. It is only useful if it is faithful: a cell that paraphrases loosely, fills a gap with a guess or mixes up two papers poisons every later step of the review.
</context>

<task>
Build a matrix from these sources:
<papers>
[PAPERS]
</papers>

Columns: citation, research question, design, sample and setting, measures, key findings, limitations

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
