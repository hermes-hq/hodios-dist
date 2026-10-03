---
name: critique-slide-deck
description: Critiques a slide deck for storyline, one idea per slide, text density and visual clarity, and returns ranked slide-level fixes with rewritten titles. Use before presenting or sending a deck.
license: CC0-1.0
arguments:
  - deck
  - audience
argument-hint: <deck> [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: presentations
  source: https://hermes-ide.com/prompts/critique-slide-deck
  catalog: 2026.1003.2
---

# Critique a slide deck

## Inputs

- `deck` (required): The deck as text (slide titles, bullets, chart descriptions and notes, in order), or exported slides or images if your tool can read them.
- `audience` (optional): Optional: who will see it and whether it will be presented live or read alone, for example "board, sent as a pre-read".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A deck is judged on whether the audience gets the point and acts on it. The common problems, roughly in order of damage: no clear storyline (reading the titles in order tells no story), topic-label titles instead of claims, several ideas crammed onto one slide, walls of text, charts that do not show the point (wrong chart type, no highlight, unlabelled axes, too many series), and inconsistent formatting. A deck presented live should carry less text than a deck sent as a pre-read, which must stand on its own.
</context>

<task>
Critique this deckOnly if audience was provided:  for $audience:
<deck>
$deck
</deck>

1. If the deck is empty or only a topic, ask for the slides and stop. If you only have text and cannot see the visuals, say so once and judge visuals only from their descriptions.
2. If the audience or the mode (presented or read) is not given, infer it and state your assumption.
3. Storyline test: list the slide titles in order. Can you state the deck's main message in one sentence from the titles alone? Note where the logic jumps, repeats or stalls, and where the ask or conclusion is missing or buried.
4. For each slide that has a problem, check:
   - Title: a full-sentence claim? If not, rewrite it as one using only content on the slide.
   - One idea: does everything on the slide support the title? If not, say what to split or cut.
   - Density: more than about 40 words for a live talk (or about 80 for a pre-read), or more than six bullets, is too dense; say what to cut or move to notes or an appendix.
   - Visuals: does the chart or image prove the title? Name a better chart type, the highlight to add, or the clutter to remove (gridlines, 3D, legends that could be direct labels, too many colours).
   - Accessibility: small text, low contrast or meaning carried by colour alone, where the description reveals it.
5. Rank all issues by how much they hurt the audience's understanding. Fatal: the point is unclear or wrong. Major: a slide fails its job. Minor: polish.
</task>

<constraints>
- Be specific: every issue names the slide and a concrete fix. No generic advice ("use fewer words").
- Use only the deck's content in rewritten titles; do not invent data.
- Skip slides with no problems; do not pad.
- Do not comment on brand colours or fonts unless they hurt readability.
</constraints>

<output_format>
## Verdict
Three lines: the deck's main message as you understand it, its biggest problem, and whether it is ready to present (ready / ready after fixes / needs restructuring).
## Storyline
The titles in order, then what the storyline does well and where it breaks.
## Slide-by-slide
A table: Slide | Issue | Fix (including any rewritten title) | Severity.
## Top changes
The three changes that would most improve the deck, in order.
</output_format>
