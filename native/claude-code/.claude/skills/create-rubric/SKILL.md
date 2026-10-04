---
name: create-rubric
description: Builds an analytic rubric with distinct criteria, performance levels and observable descriptors aligned to learning objectives, plus scoring notes. Use when setting or marking an assignment.
license: CC0-1.0
arguments:
  - assignment
  - levels
  - objectives
argument-hint: <assignment> [levels] [objectives]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/create-rubric
  catalog: 2026.1004.0
---

# Create an analytic rubric

## Inputs

- `assignment` (required): The assignment brief students receive, including the task and any length or format requirements.
- `levels` (optional; default: 4): Number of performance levels, from 3 to 6.
- `objectives` (optional): Optional learning objectives the assignment assesses. Without them, objectives are inferred from the brief and listed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most rubrics fail in the descriptors. "Excellent analysis / good analysis / some analysis / poor analysis" tells a student nothing and lets two markers give different scores to the same work. A reliable analytic rubric has a few criteria that do not overlap, descriptors that name what can be seen in the work, and levels that differ in quality along the same dimension rather than in quantity alone.
</context>

<task>
Build an analytic rubric with $levels performance levels for this assignment:

<assignment>
$assignment
</assignment>
Only if objectives was provided: 
<objectives>
$objectives
</objectives>

1. List the objectives the assignment assesses. If none were given, infer them from the brief and mark them "inferred".
2. Choose 3 to 6 criteria. Each criterion assesses one thing; no two criteria reward the same feature (for example, do not grade evidence under both "Argument" and "Use of sources"). Separate content from mechanics.
3. Name the levels from highest to lowest (e.g. Exceeds, Meets, Approaching, Beginning for 4 levels).
4. Write each descriptor so that a marker can point to evidence in the work:
   - Describe what is present, not just adjectives. "Each claim is supported by a cited source and an explanation of how it supports the claim" rather than "Strong evidence".
   - Keep descriptors parallel: the same dimensions appear at every level, varying in quality.
   - Write the "meets" level first as the target, then the levels around it.
   - Avoid counting-only descriptors ("3 sources") unless the count is the requirement.
5. Weight the criteria by importance to the objectives and give point ranges per level.
6. Write scoring notes: how to decide between adjacent levels for the criteria where markers are most likely to disagree, and what to do with work that does not fit any descriptor.
</task>

<constraints>
- Every criterion must map to at least one objective, and every objective must be assessed by at least one criterion.
- Use language students can understand; the rubric will be shared with them.
- If the assignment brief is too vague to define criteria (e.g. "a project about the environment"), ask up to three questions and stop.
- If $levels is outside 3 to 6, use the nearest of those and say so.
</constraints>

<output_format>
## Objectives assessed
Numbered list.
## Rubric
A Markdown table: Criterion (weight) | one column per level, highest first, with points in the header. Descriptors in full sentences.
## Alignment
A table: Criterion | Objectives it assesses.
## Scoring notes
Bullets for borderline decisions, then a one-line student-facing version of the top-level descriptor for each criterion, for use as a checklist.
</output_format>
