---
name: generate-realistic-seed-data
description: Generates realistic, referentially consistent fixture data for a database schema, with labelled edge cases and no real personal data. Use for local development, demos and integration tests.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/generate-realistic-seed-data
  catalog: 2026.1002.0
---

# Generate realistic seed data

## Inputs

- [SCHEMA] (required): CREATE TABLE statements or an ORM model definition, including constraints, enums and foreign keys.
- [ROW_COUNTS] (optional; default: 20 per table): Rows to generate, overall or per table, for example "5 users, 30 orders".
- [FORMAT] (optional; one of: sql, csv, json; default: sql): Output format.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Seed data is only useful if it loads and if it looks like production. Typical generated fixtures fail on the first foreign key, use "test1, test2" names that hide layout bugs, give every customer exactly one order, and leave out the rows that break code: the longest name, the null middle name, the order with no items, the timestamp on a daylight-saving boundary. Fixtures also leak real personal data when someone copies production rows. Good seed data obeys every constraint, has realistic skew and ordering, deliberately includes edge cases, and is fictitious by construction.
</context>

<task>
Generate [ROW_COUNTS] of seed data as [FORMAT] for:
[SCHEMA]

1. Parse the schema. Order tables so every referenced row exists before it is referenced. Break cycles, such as a self-referencing manager_id, by inserting with nulls and updating afterwards, or with deferred constraints where the engine supports them.
2. Satisfy every constraint: types, lengths, NOT NULL, UNIQUE, CHECK, enums and foreign keys.
3. Make it realistic:
   - skewed relationships (a few customers with many orders, most with one or two);
   - timestamps in a consistent order (created before updated, ordered before shipped) relative to a fixed anchor date you state;
   - derived values that agree (an order total equals the sum of its lines);
   - varied, plausible, invented names and text in several locales.
4. Include edge cases on purpose and label them in the Notes: maximum-length strings, accented, non-Latin, emoji and right-to-left text, empty strings versus nulls where both are allowed, zero and boundary numbers, timestamps at month end, leap day and daylight-saving transitions, soft-deleted rows, and parents with no children.
5. Make it deterministic: fixed ids and dates, so tests can rely on specific rows.
6. Output: for sql, INSERT statements in dependency order inside one transaction; for csv, one block per table with a header row; for json, one object keyed by table name.
7. If the requested volume is too large to list usefully (more than a few hundred rows in total), write a small hand-made set with the edge cases plus a deterministic, seeded generator for the bulk, and say why.
</task>

<constraints>
- No real people, real companies' customer data, real addresses or working contact details. Use reserved example domains (example.com, example.org, example.net), fictional phone ranges such as 555-0100 to 555-0199 in North America, documentation IP ranges (192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24), and payment card numbers only from published test ranges.
- For national identifiers and similar sensitive fields, use values that are structurally invalid or from documented test ranges, and say so.
- If a column's meaning is unclear (a polymorphic type column, a JSON payload with no schema), ask or state the assumption.
</constraints>

<output_format>
## Notes
The insertion order, the anchor date, how cycles were broken, and a list of edge cases with the rows that carry them.

## Data
The data in [FORMAT], in fenced blocks.

## Constraint check
One line per constraint, saying how the data satisfies it.
</output_format>
