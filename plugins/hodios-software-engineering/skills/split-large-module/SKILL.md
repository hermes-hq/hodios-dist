---
name: split-large-module
description: Maps the responsibilities and internal dependencies of an oversized file or class and plans its split into cohesive modules, in small steps that keep tests green. Use before breaking up a god class.
license: CC0-1.0
arguments:
  - file
  - constraints
argument-hint: <file> [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/split-large-module
  catalog: 2026.1004.0
---

# Plan splitting a large module

## Inputs

- `file` (required): The oversized file or class, pasted or as a path, plus how it is imported elsewhere if you know.
- `constraints` (optional): Limits on the split, for example a public API that must not change, a deadline, one PR per week, or modules the team already has.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A file grows large because several responsibilities share it, and they are usually tangled through shared private state and helper functions. Splitting by line count or alphabetically produces modules that still depend on each other in both directions. A good split groups code by the data it touches and the reasons it changes, follows the real dependency graph so the new modules have no cycles, and happens in steps small enough that each one can be reviewed, merged and reverted on its own.
</context>

<task>
Plan how to split:
$file
Only if constraints was provided: Constraints: $constraints

1. Inventory the members (functions, methods, fields, constants, types). For each, record what state it reads and writes, what it calls, and who calls it from outside the file (search the repository if you can).
2. Cluster members into responsibilities by shared data and shared reasons to change. Name each cluster by what it does in the domain, not by technical layer. Flag members that belong to no cluster or to several.
3. Draw the dependency map between clusters, marking each edge with the members that create it. Find cycles and the shared state that causes them.
4. Propose target modules: name, responsibility in one sentence, public surface, and the state it owns. Break each cycle explicitly: move the shared piece to the lower module, pass it as a parameter, or introduce a small interface. Keep the original file as a facade that re-exports the old public API, so callers do not change until a final, optional step.
5. Order the steps so that every step compiles, passes tests and changes one thing: extract leaf clusters (no outgoing dependencies) first, move one cluster per step, update internal references, and remove the facade last. For each step, say what moves, the verification command, and how to revert.
6. Check the safety net: if the tests do not cover a cluster's behaviour, add a step before moving it to add characterization tests for that cluster.
</task>

<constraints>
- This is a plan. Do not perform the moves or rewrite the code.
- No step may change behaviour. Renames, signature changes and bug fixes are separate, later steps if they are needed at all.
- Prefer fewer, cohesive modules over many tiny ones; justify any module with fewer than three members.
- If the file is not available in full, say which parts you could not see and how that limits the plan.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Responsibilities
Table: Cluster | Members | State it owns | Reason it changes.
## Dependency map
A Mermaid flowchart of clusters with labelled edges, then the cycles found and how each is broken.
## Target modules
Table: Module (path) | Responsibility | Public surface | Depends on.
## Step plan
Numbered steps. Each: what moves, verification command, revert, approximate diff size.
## Risks
Bullets: dynamic access, reflection, serialization or import side effects that could break, plus gaps in test coverage.
</output_format>
