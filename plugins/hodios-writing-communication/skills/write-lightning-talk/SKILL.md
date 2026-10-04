---
name: write-lightning-talk
description: Writes a five-minute lightning talk or a timed PechaKucha or Ignite script around one idea, with slide-by-slide words, visuals and a closing line, for meetups and internal demos.
license: CC0-1.0
arguments:
  - topic_and_point
  - format
argument-hint: <topic_and_point> [format]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: presentations
  source: https://hermes-ide.com/prompts/write-lightning-talk
  catalog: 2026.1004.1
---

# Write a lightning talk

## Inputs

- `topic_and_point` (required): What the talk is about, the one point you want people to leave with if you know it, and your material (story, example, data, demo) plus who the audience is.
- `format` (optional; one of: lightning-5min, pechakucha-20x20, ignite-20x15; default: lightning-5min): lightning-5min is free-paced, 5 minutes; pechakucha-20x20 is 20 slides auto-advancing every 20 seconds; ignite-20x15 is 20 slides auto-advancing every 15 seconds.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Short formats punish the habits of long talks. There is no time for an agenda, a bio slide or three points; a lightning talk has room for one idea, one story or example that makes it concrete, and one line people remember. Auto-advancing formats add a second constraint: each slide gets the same fixed time, so every slide's words must fit it, and the slides should be images that the words explain, not text to read. Speakers run over most often by squeezing in "one more thing" and by unrehearsed transitions.
</context>

<task>
Write a talk in the $format format.

<topic_and_point>
$topic_and_point
</topic_and_point>

Timing by format, at about 130 spoken words a minute:
- lightning-5min: 5:00 hard stop, so aim for about 4:30: about 550 to 600 words, 6 to 12 slides at the speaker's pace.
- pechakucha-20x20: 20 slides × 20 seconds = 6:40, about 40 to 45 words per slide.
- ignite-20x15: 20 slides × 15 seconds = 5:00, about 30 to 33 words per slide.

1. If there is no material to build from (no story, example, data or experience), ask for one and stop.
2. State the one idea in a single sentence. If the material holds several ideas, choose the strongest for this audience and list what you cut.
3. Choose a shape: problem → turn → payoff, before → after, a single story with a lesson, or a myth and its correction. Say which and why.
4. Write the script slide by slide: the visual for each slide (an image, a single number, a short phrase or a demo frame) and the exact words to say, within that format's word budget.
5. Write a closing line that restates the idea in a memorable form, and the last slide.
6. Add rehearsal notes: where timing is tight, which slides are buffers, and what to do if a slide advances before you finish.
</task>

<constraints>
- One idea. No agenda slide, no "about me" slide longer than one sentence of spoken words, no "any questions?" slide in auto-advancing formats.
- Spoken language: short sentences, concrete nouns, and transitions that hand off to the next slide ("Which is exactly what broke on Tuesday.").
- In PechaKucha and Ignite, every slide's word count must fall within its budget; show the count.
- Slides carry at most a few words; the speaker carries the meaning.
- Use only facts, numbers and stories from the material. Mark anything the talk needs but lacks as `[NEEDED: …]`.
- A live demo inside five minutes needs a recorded fallback; say so if a demo is planned.
</constraints>

<output_format>
## The one idea
One sentence, then "Cut:" with anything left out.
## Shape
One or two lines.
## Script
A table: Slide | Visual | Words (with word count in brackets).
## Closing line
The last sentence, word for word.
## Rehearsal notes
Three to five bullets, including total word count against the time budget.
</output_format>
