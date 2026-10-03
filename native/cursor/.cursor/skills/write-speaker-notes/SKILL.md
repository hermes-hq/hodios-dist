---
name: write-speaker-notes
description: Writes natural, speakable notes for each slide with a time budget, the one point to stress and a transition to the next slide, and checks the total fits the time slot.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: presentations
  source: https://hermes-ide.com/prompts/write-speaker-notes
  catalog: 2026.1003.2
---

# Write speaker notes

## Inputs

- [SLIDES] (required): The slide content in order, as text: titles, bullets, chart descriptions, and any notes you already have. Number the slides if you can.
- [MINUTES] (optional; default: 15): Total speaking time in minutes, excluding Q&A.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Speaker notes are for glancing at under pressure, not for reading aloud. The worst notes repeat the slide text, so the speaker reads the slide to an audience that has already read it. Good notes add what the slide does not say (the meaning of the chart, the example, the "so what"), use short spoken sentences, mark the one thing that must land, and carry a transition so the talk flows instead of restarting at every slide. Most people speak at about 130 to 150 words a minute in a presentation, slower with pauses.
</context>

<task>
Write speaker notes for these slides, for a [MINUTES]-minute talk:
<slides>
[SLIDES]
</slides>

1. If the slides are empty or are only a topic, ask for the slide content and stop.
2. Budget the time: give each slide minutes in proportion to its weight (the key evidence slide gets more than the title slide), keep about 10% buffer, and track a running total.
3. For each slide write:
   - **Stress:** the one point the audience must take away, in one sentence.
   - **Notes:** what to say, in short spoken sentences and contractions, adding meaning beyond the slide text. Explain charts by their point ("Look at the right edge: that's the week we changed the price"). Mark [pause] where a point needs to land and [click] for builds or animations if the slide text implies them.
   - **Transition:** one sentence that links to the next slide's point.
4. Size each slide's notes to its time at about 130 words a minute. Notes for a slide with one minute should be under about 130 words.
5. Write the first and last slides more fully: the opening lines and the closing lines are worth having word for word.
</task>

<constraints>
- Use only content from the slides. Where a slide needs an example, story or number to make its point and none is given, write `[example needed: …]` instead of inventing one.
- Do not repeat the slide's bullets verbatim in the notes.
- Natural speech: no long subordinate clauses, no reading out of URLs or long numbers in full (round only if the slide already rounds).
- If the slides cannot fit the time (for example 30 dense slides in 10 minutes), say so in Timing check and suggest which slides to cut or merge.
</constraints>

<output_format>
## Speaker notes
For each slide: "### Slide N: <title> (m:ss, total m:ss)", then Stress, Notes and Transition.
## Timing check
Total words, estimated time at 130 words a minute, buffer left, and any slides to cut or merge.
## Gaps
Bullets: `[example needed]` items. "None" if none.
</output_format>
