---
name: explain-codebase
description: Explains an unfamiliar codebase. Maps its structure, traces one real request end to end and names the concepts and gotchas a newcomer needs. Use when joining a project or reading an unknown repo.
license: CC0-1.0
arguments:
  - focus
  - depth
  - background
argument-hint: "[focus] [depth] [background]"
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: learning
  source: https://hermes-ide.com/prompts/explain-codebase
  catalog: 2026.1004.3
---

# Explain a codebase

## Inputs

- `focus` (optional): A feature, flow or question to centre the explanation on (for example "how a payment is captured"). Leave empty for a general tour.
- `depth` (optional; one of: overview, deep; default: overview): overview gives the map and one flow; deep also covers data model, error handling, configuration and tests.
- `background` (optional): What the reader already knows, such as the language or framework, so the explanation skips it.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A newcomer does not need a summary of every file. They need a mental model: what the system is for, where each responsibility lives, how one real piece of work travels through the code, and which surprises will cost them a day. Explanations of code are only useful if they are true, so every statement must point at the file that proves it.
</context>

<task>
Explain the codebase in the working directory at $depth depth.
Only if focus was provided: 
Centre the explanation on: $focus
Only if background was provided: 
The reader already knows: $background. Do not explain that.

1. Orient: read the README, contributing docs, manifests and lockfiles (languages, frameworks, key dependencies), build and CI config, and the top two levels of the directory tree. Skip vendored, generated and build output folders.
2. Find the entry points: main functions, server bootstrap, CLI definitions, route tables, job schedulers, exported library index.
3. Trace one real flow from entry to exit (the focus, if given, or the most central user action): each hop with `path:line`, what it does and what data it passes on.
4. Identify the key concepts: domain terms, core types or tables, and the architectural pattern actually used (layers, modules, events), described from the code, not from labels.
5. For deep: also cover the data model, error handling, configuration and environment variables, and how the tests are organised and run.
6. Note gotchas: code generation, magic or convention-based wiring, global state, surprising side effects, environment-dependent behaviour, dead or legacy areas.
</task>

<constraints>
- Cite a file path (and line where useful) for every claim about the code. Mark anything inferred from names or structure rather than read as "(inferred)".
- Do not describe files you have not opened as if you had. If the repo is too large to read fully, say which parts you sampled.
- Do not suggest refactors or fixes unless the reader asks; this is an explanation.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## What it is
Two or three sentences: purpose, users, main technologies.
## Map
A table: directory or module | responsibility | files to read first.
## How a request flows
Numbered hops with `path:line`. Add a Mermaid sequence or flowchart if there are more than five hops.
## Key concepts
A short glossary of domain terms and core types, each with where it is defined.
## Where to start
Three files to read first, and one small, safe change that would teach the reader the workflow (for example adding a test for an existing function).
## Gotchas
Bullets, each with the file that shows it.
## Open questions
What the code alone could not answer, and who or what might (docs, history, owners).
</output_format>
