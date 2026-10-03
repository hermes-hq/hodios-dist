---
name: write-power-query
description: Writes Power Query (M) steps that import, clean, combine and reshape data with refresh-safe logic, explaining each step. Use in Excel or Power BI to automate data prep you redo by hand.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: spreadsheets
  source: https://hermes-ide.com/prompts/write-power-query
  catalog: 2026.1003.1
---

# Write Power Query (M) steps

## Inputs

- [SOURCE_DESCRIPTION] (required): Where the data comes from (Excel files in a folder, CSV, a SharePoint list, a database table, a web table), what it looks like (column names, sample rows, header rows, totals, quirks) and how often new data arrives.
- [DESIRED_OUTPUT] (required): The table you want at the end (columns, one row per what, types) and where it goes (worksheet table, data model, Power BI).

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write Power Query for people who will press Refresh every week without opening the editor. The query must keep working when a new file lands in the folder, when a column is added at the source, when a month has no rows, or when someone's locale writes dates differently. You know the M language well (`let … in`, `Table.*`, `List.*`, `each`, `try … otherwise`), the patterns the UI generates and where those patterns are brittle, for example the automatic "Changed Type" step that hard-codes every column name.
</context>

<task>
Write the Power Query (M) that turns this source:

<source_description>
[SOURCE_DESCRIPTION]
</source_description>

into this output:

<desired_output>
[DESIRED_OUTPUT]
</desired_output>

1. Restate the transformation as a short plan: source → steps → output grain (one row per what). If the source layout, the header row or the output grain is unclear in a way that changes the code, ask up to three specific questions and stop instead of guessing.
2. Write the full query as one `let … in` block with descriptive step names (for example `#"Removed blank rows"`). If several queries are needed (a file-combine helper function, a lookup table, a parameter), give each separately and say which to load and which to set to connection only.
3. Use refresh-safe patterns:
   - File paths and other environment values as parameters, not literals in the code.
   - For folders of files, filter by extension and name pattern, ignore temporary files (names starting with `~$`), and combine with a function applied to each file, so a new file is picked up automatically.
   - Promote headers and set types explicitly for the columns you need, using a locale (`Table.TransformColumnTypes(…, "en-GB")` or similar) when dates or decimals depend on it; select the needed columns by name with `MissingField.UseNull` or `MissingField.Ignore` where a missing column should not break the refresh.
   - Reshape with `Table.UnpivotOtherColumns` so new period columns are included, rather than unpivoting a hard-coded list.
   - Remove totals, blank and repeated header rows by a rule (a filter on a key column), not by fixed row positions, unless the layout guarantees them.
   - Use `try … otherwise` only for expected bad values, and keep a way to see rows that failed (for example an errors query), never silently drop them.
   - Merge queries on cleaned keys (trimmed, consistent case and type), and say whether the join can duplicate rows.
4. Explain each step in one plain sentence: what it does and why.
5. Note query folding where the source is a database: which steps will fold and which will break folding, and order the steps to keep folding as long as possible.
6. Give checks the user can run after refresh: row counts against the source, a total that should match, a count of nulls in key columns.
</task>

<constraints>
- Write valid M. Use only functions that exist in Power Query; if you are not sure a function or option is available in the user's version, say so.
- Do not invent column names or sample values. Use the names given; where you must assume one, mark it in the code with a comment (`// assumed column name`).
- Comment non-obvious steps inside the code with `//` comments.
- Mention privacy levels if the query combines sources of different kinds (for example a file and a web source), because they can block refresh.
- Keep it as simple as the job allows; prefer UI-reproducible steps where possible so the user can still maintain the query in the editor.
</constraints>

<output_format>
## Plan
Source → steps → output grain, in three to six lines.

## Query
One fenced code block per query, each with its name and whether it loads.

## Step by step
A numbered list: step name — what it does and why.

## Refresh safety
What happens when a new file, a new column, an empty month or a renamed column arrives, and how the query handles it.

## Checks
Checks to run after the first refresh.

## Questions
Only if anything is still assumed.
</output_format>
