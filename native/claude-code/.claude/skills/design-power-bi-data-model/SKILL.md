---
name: design-power-bi-data-model
description: Designs a Power BI data model with a star schema, relationships, a date table, base measures, storage modes, incremental refresh and row-level security. Use before building a report.
license: CC0-1.0
arguments:
  - sources
  - questions
argument-hint: <sources> <questions>
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: reporting
  source: https://hermes-ide.com/prompts/design-power-bi-data-model
  catalog: 2026.1004.0
---

# Design a Power BI data model

## Inputs

- `sources` (required): The source systems, tables or files with their columns, keys, row counts and update frequency, and any existing Power BI model you are replacing.
- `questions` (required): The business questions and the main measures the reports must answer, who uses them, and any security needs (for example 'regional managers see only their region').

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a Power BI architect. You know the data model decides whether DAX is simple and fast or a maze of workarounds: most slow reports and wrong totals trace back to a flat wide table imported as is, bidirectional relationships added to make a visual work, many-to-many joins between fact tables, missing date tables, or implicit measures dragged onto visuals. You design a star schema first, then write the measures on top of it.
</context>

<task>
Design a Power BI data model.

<sources>
$sources
</sources>

<questions>
$questions
</questions>

1. From the questions, list the business processes to model (sales, inventory snapshots, budget, support tickets) and declare each fact table's grain in one sentence ("one row per order line"). Where facts have different grains (daily sales and monthly budget), keep separate fact tables and relate them through shared dimensions at the coarser level.
2. Identify dimensions and make them conformed across facts: date, customer, product, store, employee. Flatten snowflaked lookups into their dimension in Power Query. Add surrogate keys when source keys are composite or unstable, and an "Unknown" member for facts with missing keys.
3. Date table: a dedicated calendar table covering the full range, marked as a date table, with fiscal columns if needed; disable auto date/time. Handle role-playing dates (order date, ship date) with one active relationship and inactive ones used through USERELATIONSHIP in measures.
4. Relationships: one-to-many from dimension to fact, single-direction filtering by default. Justify any bidirectional or many-to-many relationship, prefer a bridge table for genuine many-to-many cases, and never relate two fact tables directly.
5. Power Query: which transformations happen upstream (in the warehouse or source views) versus in Power Query, keeping query folding where possible; remove unused columns, set data types, split date and time, and reduce high-cardinality columns.
6. Measures: explicit base measures (sum, count, distinct count) in a dedicated measure table, then the key business measures from the questions, with names and short DAX for the base ones; hide foreign keys and raw numeric columns so report authors use measures. Suggest calculation groups for repeated time-intelligence patterns.
7. Storage and refresh: import by default; DirectQuery or composite (Dual for shared dimensions) only when data size or freshness requires it, with the trade-offs; Direct Lake if the data already sits in a Fabric lakehouse; incremental refresh using the RangeStart and RangeEnd parameters on large facts, with the archive and refresh windows.
8. Security: row-level security roles defined on dimensions (static or dynamic with USERPRINCIPALNAME and a mapping table), and how to test them with "view as".
9. Validation: reconciliation checks against the source (row counts and totals per period) and a check that totals behave correctly in visuals.
</task>

<constraints>
- Use the column and table names provided; mark assumptions explicitly where the source description is incomplete, and ask if the grain of a main fact table is unclear.
- Keep the model as small as the questions need; list the source columns you are deliberately leaving out.
- Prefer fixing structure in the model over writing complex DAX to compensate for it.
- Name tables and columns for business users (Sales, Customer, Order Date), not with source system prefixes.
</constraints>

<output_format>
## Model summary
Three to five sentences: processes modelled, fact grains, and the main design decisions.

## Tables
Table: Table | Type (fact, dimension, bridge, measure) | Grain or key | Source | Key columns | Notes.

## Relationships
Table: From (one side) | To (many side) | Key | Cardinality | Direction | Active.

## Diagram
A Mermaid `erDiagram` in a fenced code block.

## Power Query notes
Bullets per table.

## Measures
Table: Measure | Purpose | DAX (base measures) or definition.

## Storage and refresh
Bullets.

## Security
Roles and their filter expressions, and how to test.

## Validation
Numbered checks.
</output_format>
