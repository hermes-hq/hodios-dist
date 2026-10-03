---
name: plan-monolith-extraction
description: Plans extracting one capability from a monolith with the strangler-fig pattern, covering seams, data ownership, traffic shifting and rollback at every step. Use before splitting a service out.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: migration
  source: https://hermes-ide.com/prompts/plan-monolith-extraction
  catalog: 2026.1003.0
---

# Plan extracting a service from a monolith

## Inputs

- [MONOLITH] (required): The monolith - stack, size, deployment, database, teams that work in it, and the pain that motivates the extraction.
- [CAPABILITY] (required): The capability to extract - what it does, its code locations, the tables it reads and writes, and who calls it.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most extractions that go wrong end as a distributed monolith: a new service that still shares the old database, makes chatty synchronous calls back into the monolith, and must deploy in lockstep with it. The strangler-fig pattern avoids this by first carving a clean seam inside the monolith, then moving ownership of the data, then shifting traffic gradually with a rollback at every step. The hardest part is almost always the data, not the code.
</context>

<task>
Plan extracting this capability:
[CAPABILITY]
from this monolith:
[MONOLITH]

1. Should you extract? Weigh the stated motivation (independent deploys, team autonomy, scaling or isolation needs) against the cost (network calls, consistency, operations, on-call). If a modular boundary inside the monolith would solve the problem, say so plainly and give the plan anyway, so the team can decide.
2. Map the current state: code entry points, inbound callers, outbound dependencies, and the tables the capability writes, reads, and shares with other modules. Where the description is not enough, list what to find in the code under Open questions.
3. Define the target boundary: the service's API or events, which calls become asynchronous, and the consistency each caller gets.
4. Plan data ownership: which tables move, a single writer for every table at every phase, how other modules that read these tables switch to the API or to events, and how data stays in sync during transition (change data capture or a transactional outbox). Replace cross-boundary transactions with sagas or compensating actions where needed.
5. Phase the work, each phase shippable and reversible:
   - Build a seam inside the monolith (branch by abstraction) and route all access through it.
   - Stand up the service behind a routing facade, running in shadow mode with results compared.
   - Move reads, then writes, by percentage or by tenant.
   - Move data ownership, then remove the old code and tables.
6. For each phase, give exit criteria and the rollback.
7. List operational readiness: monitoring and SLOs, on-call ownership, contract tests, versioning, and runbooks.
</task>

<constraints>
- Never leave two writers on the same table across the boundary, and never share a database between the monolith and the new service as the end state.
- Avoid a big-bang cutover. Every traffic shift must be adjustable in minutes.
- Use only the facts given; mark assumptions about code and data as assumptions.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Should you extract
A recommendation (extract, modularise first, or do not extract) with the reasoning.
## Current state
Callers, dependencies and tables, plus a Mermaid diagram.
## Target boundary
API or event contracts in outline, and the consistency model.
## Data ownership
A table: table, current writers, current readers, owner after migration, sync method during transition.
## Phases
A table: phase, change, exit criteria, rollback.
## Traffic shifting
Mechanism, increments, metrics compared, and abort conditions.
## Risks
Bullets, including the distributed-monolith traps specific to this capability.
## Open questions
What to confirm in the code or with the teams.
</output_format>
