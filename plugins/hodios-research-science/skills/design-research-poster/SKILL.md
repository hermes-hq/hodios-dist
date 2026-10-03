---
name: design-research-poster
description: Designs a conference poster with a headline finding, layout grid, condensed sections, figures to include and a 60-second walkthrough script. For researchers presenting at conferences.
license: CC0-1.0
arguments:
  - paper_or_results
  - poster_size
  - audience
argument-hint: <paper_or_results> [poster_size] [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/design-research-poster
  catalog: 2026.1003.0
---

# Design a research poster

## Inputs

- `paper_or_results` (required): The paper, abstract or results to present, with the key numbers and the figures you already have (describe each figure).
- `poster_size` (optional; default: A0 portrait): Size and orientation from the conference instructions, for example "A0 portrait", "48 x 36 inches landscape", or "e-poster 16:9 screen".
- `audience` (optional): Who will walk past, for example "specialists in my subfield", "a broad clinical conference", "mixed disciplines at a student symposium".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
People spend seconds deciding whether to stop at a poster. Posters that work state the main finding in plain words as the largest text on the page, show one or two clear figures that carry the evidence, and cut everything else to short blocks that can be read from about two metres. Posters that fail are shrunken papers: a title that names the topic but not the result, dense paragraphs, and every figure from the manuscript. Evidence-informed layouts (such as the "billboard" style with a central take-home message and a side column of supporting detail) and conventional column layouts both work if the reading order is obvious. The presenter's spoken walkthrough matters as much as the poster.
</context>

<task>
Design a $poster_size poster from this materialOnly if audience was provided:  for $audience.
<material>
$paper_or_results
</material>

1. **Headline:** write three candidate main messages: one plain-language sentence each, stating the finding (not the topic), true to the data. Recommend one. Then write a short formal title for the programme listing if the conference requires one.
2. **Layout:** choose a layout (billboard with a central message, or two to four columns) suited to the size and orientation, and describe a grid with each block's position, its approximate share of the area, and the reading order. Include where the QR code, logos and author details go.
3. **Poster text:** write each block in condensed form: background (two or three sentences on the gap), question or aim, methods (bullets or a small flow diagram), results (short captions that state what each figure shows), conclusion and implications (two or three bullets), and limitations in one line. Give a word count per block and a total; aim for roughly 300–800 words depending on size.
4. **Figures:** choose the one or two figures that carry the main message and say how to adapt them for a poster: larger labels, fewer panels, direct labels instead of legends, colour-blind-safe palettes, and a one-line take-home caption above each. Describe any new figure needed, for example a simple bar or dot plot of the main effect.
5. **Walkthrough script:** a 60-second spoken version (about 150 words) that opens with the question and finding, points at the figures in order, and ends with an invitation to discuss, plus a 10-second version for passers-by.
6. **Final checks:** text size guidance for the format (for a printed poster, title roughly 85 pt or larger and body text at least 24 pt, readable from two metres), contrast, alignment, the conference's rules, a QR code to the paper or slides, and having a few printed handouts or a link.
</task>

<constraints>
- Use only the findings and numbers given. Do not round or restate numbers in a way that changes their meaning, and keep caveats (pilot study, small sample, preliminary) visible.
- The headline must be supported by the results; if the results are mixed or null, write a headline that says so honestly.
- Do not invent figures or data for them; propose figures only from the data provided.
- If the material is too thin to design from (for example only a title), ask for the abstract and key results.
- Use plain words in the headline and conclusions; keep technical terms in the methods.
</constraints>

<output_format>
Use the contract's section headings. Layout as a table: block | position | share of area | contents. Poster text as headed blocks with word counts. Figures as numbered items. Walkthrough script as quoted text. Final checks as a checklist.
</output_format>
