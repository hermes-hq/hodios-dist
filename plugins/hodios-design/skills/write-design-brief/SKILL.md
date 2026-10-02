---
name: write-design-brief
description: Writes a one-page creative brief with objective, audience, single key message, deliverables, mandatories, constraints, references and success criteria. Use before commissioning design work.
license: CC0-1.0
arguments:
  - project
  - brand
  - deadline
argument-hint: <project> [brand] [deadline]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: graphic-design
  source: https://hermes-ide.com/prompts/write-design-brief
  catalog: 2026.1002.1
---

# Write a creative brief for a designer

## Inputs

- `project` (required): What needs designing and why, who it is for, where it will appear, and anything already decided.
- `brand` (optional): Brand guidelines, assets available (logo files, fonts, colours, photography) and tone. Optional.
- `deadline` (optional): Final delivery date and any interim dates, e.g. "concepts by 3 March, final files by 17 March". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most bad design work starts with a bad brief: "make it modern and eye-catching", five things to say with equal weight, no sizes, no deadline for feedback, and an approver who appears at the final round with new opinions. A good brief is short, makes the hard choices up front (one objective, one key message, one primary audience), lists exactly what files are needed, and says how the work will be judged.
</context>

<task>
Write a creative brief for this project.

<project>
$project
</project>
Only if brand was provided: 
<brand>
$brand
</brand>
Only if deadline was provided: Deadline: $deadline
If no deadline was given, write "TBD" for it and list it in Open questions.

1. **Background:** the situation in 2 to 4 sentences: why this work, why now.
2. **Objective:** one sentence describing what the design must make the audience think, feel or do, measurable where possible ("increase workshop sign-ups from the flyer QR code"). If the input has several objectives, rank them and make the first one primary.
3. **Audience:** the primary audience, what they already believe, and the context in which they will see the work (walking past a poster, scrolling a feed, reading a 40-page report).
4. **Key message:** the single most important thing to communicate, in one sentence, plus up to three supporting points in priority order.
5. **Tone:** 3 adjectives with a "not" for each ("confident, not arrogant").
6. **Deliverables:** a table of every file needed: item, format, dimensions or size, colour space (CMYK or RGB), quantity, and where it will be used. Include source files if they are needed.
7. **Mandatories:** what must appear (logo, legal lines, URL, QR code, accessibility requirements) and brand rules that apply.
8. **Constraints:** budget, print or platform specifications (bleed, safe zones, file size limits), languages, and anything off-limits.
9. **References:** what references or competitors to look at, and what to take from each, or the gap the designer should fill if none were given.
10. **Success criteria:** how the work will be judged at review, matching the objective.
11. **Timeline and approvals:** milestones (concepts, revisions, final), number of revision rounds, who gives feedback and who approves.
12. Where the input is missing something important, write "TBD" in that field instead of inventing it, and add a question.
</task>

<constraints>
- Fit the brief on about one page. Cut anything that does not help the designer make a decision.
- Do not prescribe the design solution (layouts, colours, imagery) unless it is a brand rule. Describe the problem and the constraints.
- Do not invent budgets, dates, specifications or brand rules.
- Lead with the answer. Add reasoning only where it changes what the reader will do.
- No preamble, no restating the request and no closing summary on a short answer.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings, in order. Deliverables as a table. Open questions last, as a numbered list for the person commissioning the work.
</output_format>
