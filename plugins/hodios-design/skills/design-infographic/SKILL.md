---
name: design-infographic
description: Plans an infographic around one message, with the information hierarchy, chart and icon choices, a layout in zones, the copy and source notes. Use when turning data or a story into a single graphic.
license: CC0-1.0
arguments:
  - data_or_story
  - format
argument-hint: <data_or_story> [format]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: graphic-design
  source: https://hermes-ide.com/prompts/design-infographic
  catalog: 2026.1003.1
---

# Plan an infographic

## Inputs

- `data_or_story` (required): The data, facts or process to show, with sources, plus the audience and where it will be published. Paste the numbers; the prompt will not supply them.
- `format` (optional; default: portrait social post, 1080x1350 px): The output format and size, for example "vertical social post 1080x1350", "A3 poster", "long-scroll web graphic" or "16:9 slide".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most infographics are a vertical stack of unrelated facts, icons and big numbers with no point, and often a misleading chart: a truncated axis, a 3D pie, icons scaled by height so the area exaggerates the difference, or numbers with no source. A good infographic makes one point that a reader gets in five seconds, then supports it with a few pieces of evidence arranged in a clear order, and is honest about where every number comes from.
</context>

<task>
Plan an infographic for this format: $format.

<data_or_story>
$data_or_story
</data_or_story>

1. **The message.** Write the one sentence the reader should remember, as a headline with a verb ("Cycling to work has doubled in our city since 2015"). Give two alternatives with different angles and recommend one for the audience. If the data does not support a clear message, say so and suggest what is missing.
2. **Data check.** List every figure you will use with its source, date and unit. Flag figures with no source, mixed time periods or definitions, percentages without a base, and comparisons that are not like for like. Do not use any figure that was not supplied.
3. **Hierarchy.** Three levels: the headline and the hero visual (the one chart or figure that proves the message), 2 to 4 supporting points, and details (footnotes, method, sources). Cut anything that does not support the message and list what was cut.
4. **Visual choices.** For each data point, choose the form and explain it: a single big number with context for one figure; a bar chart for comparisons (axis starting at zero); a line for change over time; a stacked bar or waffle chart for parts of a whole (pie charts only for two or three parts); a map only when geography matters; a flow or timeline for processes; an icon array for counts of people. Avoid 3D, area-scaled pictograms and dual axes. Choose icons only where they aid recognition, in one consistent style.
5. **Layout.** Describe the layout zone by zone in reading order for the format: the headline zone, hero visual, supporting points, and footer with sources and logo. Say how the eye moves through it, the grid, approximate proportions of each zone, and how the design adapts if it must also appear as a square crop or a slide.
6. **Copy.** Write every piece of text: headline, subheading, chart titles that state the finding, labels and annotations, supporting points of no more than 15 words each, footnotes and the source line. Keep the total word count low for the format.
7. **Style notes.** Colour use (a neutral base, one highlight colour for the key data, colours that stay distinguishable for colour-blind readers), type hierarchy with sizes relative to the format, and minimum text size readable on a phone if published on social media.
8. **Accessibility.** Alt text (a short description of the message and key figures) and a longer text equivalent for the web, contrast, and not relying on colour alone.
</task>

<constraints>
- Never invent, round in a misleading way or extrapolate figures. If a key number is missing, write [figure needed] and say where it might be found.
- Charts must not distort: bars start at zero, consistent scales across compared charts, areas proportional to values.
- Keep claims within what the data shows; correlation is not presented as causation.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings. The data check as a table: | Figure | Value | Source | Date | Issue |. The layout as a numbered list of zones from top to bottom. The copy as a list keyed to the zones.
</output_format>
