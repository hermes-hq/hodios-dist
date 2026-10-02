---
name: design-database-schema
description: Designs a relational schema from requirements and access patterns, with keys, constraints, types, indexes and DDL. Use when starting a new service or feature that stores data.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/design-database-schema
  catalog: 2026.1002.2
---

# Design a relational database schema

## Inputs

- [REQUIREMENTS] (required): What the system must store and do. Entities, rules, volumes, retention and any multi-tenancy.
- [ACCESS_PATTERNS] (optional): The main reads and writes with rough frequency, for example "list a customer's last 20 orders, 200/s".
- [DATABASE] (optional; one of: postgres, mysql, sqlite, sql-server, other; default: postgres): Target database engine.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A schema outlives the code around it. Mistakes such as a missing constraint, money stored as a float, a timestamp without a time zone or a tenant key left out of an index are cheap on day one and expensive after a year of data. The database should enforce the rules it can, so bad data cannot get in through any code path.
</context>

<task>
Design a [DATABASE] schema for:
[REQUIREMENTS]
Only if [ACCESS_PATTERNS] was provided: 
Access patterns:
[ACCESS_PATTERNS]

1. List the entities, their relationships and cardinalities, and the business rules the data must obey. Write down every assumption you make.
2. Model to third normal form first. Denormalise only where a listed access pattern needs it, and say which one.
3. Choose keys: a surrogate primary key (identity integer, or a time-ordered UUID when ids are created outside the database or exposed publicly), plus natural unique keys as `UNIQUE` constraints.
4. Choose types deliberately: exact decimals for money (with the currency stored alongside), time-zone-aware timestamps, text with `CHECK` constraints or lookup tables for small fixed sets, and JSON only for data that is genuinely schemaless.
5. Enforce rules in the database: `NOT NULL` by default, foreign keys with an explicit `ON DELETE` behaviour, `UNIQUE` and `CHECK` constraints.
6. Derive indexes from the access patterns, one per pattern at most, with column order explained. Index foreign keys used in joins or cascading deletes.
7. For multi-tenant data, put the tenant key in every tenant-owned table, in its unique constraints and first in its indexes.
</task>

<constraints>
- Model only what the requirements need. Add audit columns, soft deletes or history tables only when a requirement asks for them, and list them under Trade-offs as options otherwise.
- Use DDL that runs on [DATABASE] as written. Do not mix dialects.
- Every index maps to a named access pattern or foreign key.
- When a requirement is ambiguous in a way that changes the model (one-to-many or many-to-many, hard or soft delete), pick one, say so in Assumptions, and add the question to Open questions.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Assumptions
Numbered.

## Diagram
A Mermaid `erDiagram` with every table, key and relationship.

## DDL
One SQL code block that creates every table, constraint and index in dependency order.

## Access patterns
| Pattern | Query shape | Index used |

## Trade-offs
Each significant choice, the alternative, and why you chose this one.

## Open questions
Questions whose answers would change the schema. "None" if none.
</output_format>
