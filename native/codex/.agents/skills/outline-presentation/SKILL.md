---
name: outline-presentation
description: Outlines a story-driven presentation with assertion-style slide titles, using SCQA or the pyramid principle, sized to the time slot and aimed at a stated goal for a specific audience.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: presentations
  source: https://hermes-ide.com/prompts/outline-presentation
  catalog: 2026.1004.3
---

# Outline a presentation

## Inputs

- [TOPIC] (required): What the presentation is about, with your key material, findings or notes.
- [AUDIENCE] (required): Who will be in the room and what they know and care about, for example "VP-level, non-technical, sceptical about budget".
- [MINUTES] (optional; default: 15): Speaking time in minutes, excluding Q&A.
- [GOAL] (optional): What the audience should think, decide or do afterwards, for example "approve a pilot" or "understand the new process".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most decks fail before any slide is designed: they are organised by topic ("Background", "Data", "Next steps") instead of by argument, so the audience sees information but not the point. Two structures fix this. SCQA (Situation, Complication, Question, Answer) builds tension and suits persuasion and change. The pyramid principle (answer first, then the supporting arguments, each backed by evidence) suits recommendations to senior or time-pressed audiences. In both, slide titles are assertions: full-sentence claims ("Churn doubled after the price change"), not labels ("Churn"). Reading only the titles in order should tell the whole story.
</context>

<task>
Outline a [MINUTES]-minute presentation for [AUDIENCE] on:
<topic>
[TOPIC]
</topic>
Only if [GOAL] was provided: Goal: [GOAL]

1. If the topic gives no material to build an argument from (only a subject heading), ask for the key facts or findings and stop.
2. If no goal is given, infer the most likely one from the topic and audience and state it in Big idea as an assumption.
3. Write the big idea: one sentence, a claim the audience could disagree with, that the whole talk supports.
4. Choose SCQA or the pyramid and say why in one line, based on the audience and goal (for example: senior decision-makers, pyramid; an audience that does not yet see the problem, SCQA).
5. Size the deck: about one content slide per 1 to 2 minutes, plus a title slide. Allow 10% of the time as buffer.
6. Write an assertion title for each slide (at most 15 words), what goes on it (the evidence or visual that proves the title, for example "line chart, monthly churn, 2024-2025, price change annotated"), the evidence still needed, and minutes.
7. Open with a hook that matters to this audience (a number, a consequence, a question), and close on the goal: the decision or action requested, not "Questions?".
8. Check the horizontal logic: read the titles in order. If any does not follow from the one before, fix it.
</task>

<constraints>
- One idea per slide. If a slide needs two titles, split it.
- Use only facts from the topic. Where a slide needs a number or example you do not have, mark it `[data needed: …]`.
- Put supporting detail the audience may ask for in an appendix list rather than in the main flow.
- Do not design slide visuals beyond a one-line description of the chart or image.
</constraints>

<output_format>
## Big idea
One sentence, plus the goal (stated or inferred).
## Structure
SCQA or pyramid, the reason, and how the sections map to slides.
## Slide outline
A table: # | Assertion title | Content and visual | Evidence needed | Minutes. Then "Total: N minutes".
## Title read-through
The titles alone, in order, as a paragraph.
## Gaps
Bullets: `[data needed]` items and appendix slides to prepare. "None" if none.
</output_format>
