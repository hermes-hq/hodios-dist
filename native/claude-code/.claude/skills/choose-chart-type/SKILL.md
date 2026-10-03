---
name: choose-chart-type
description: Recommends the chart that best carries a specific message for a given data shape, with encodings, the alternatives considered and the anti-patterns to avoid. Use before building a chart.
license: CC0-1.0
arguments:
  - message
  - data_shape
  - audience
argument-hint: <message> <data_shape> [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data-visualization
  source: https://hermes-ide.com/prompts/choose-chart-type
  catalog: 2026.1003.2
---

# Choose a chart type

## Inputs

- `message` (required): The one point the chart must make, as a sentence (for example "Mobile overtook desktop in March and the gap is widening").
- `data_shape` (required): The variables and their types (time, category with how many levels, number), number of rows, and a few sample rows.
- `audience` (optional): Who will read it and where (an executive slide, a dashboard, a paper, a mobile screen).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a data-visualisation designer in the tradition of Cleveland, Few and the Financial Times Visual Vocabulary. A chart is chosen for the comparison it must make easy, not for the data type alone. People judge position along a common scale most accurately, then length, then angle and area, then colour intensity, so the key comparison goes on position whenever possible.
</context>

<task>
Recommend a chart.

<message>
$message
</message>

<data_shape>
$data_shape
</data_shape>

Audience and medium: $audience

If the audience is empty, assume a general business audience reading on a laptop screen.

1. Name the relationship the message is about: change over time, ranking, part-to-whole, deviation from a reference, distribution, correlation, or flow. If the message is a description of the data rather than a point ("show sales by region"), propose the two most likely points and pick one, saying so.
2. Choose the chart that puts that comparison on position or length. Typical choices: line for change over time; sorted bar (horizontal when labels are long) for ranking; slope or dumbbell chart for before-and-after; diverging bar for deviation from a target; histogram, box or strip plot for distributions; scatter for correlation; small multiples when there are more than about four series; a stacked bar or a single 100% bar for part-to-whole with few parts.
3. Specify encodings: x, y, colour, facet, ordering, the baseline, and which single element gets the highlight colour while the rest stay grey.
4. Write a title that states the message (an action title), not the variables.
5. Note the alternatives you rejected and why, and the anti-patterns specific to this data.
</task>

<constraints>
- Bars start at zero. Line charts may use a non-zero baseline when the message is about change, and the axis must make that visible.
- Avoid pie and donut charts for more than three parts or for comparing similar shares; avoid 3D, dual y-axes (offer an indexed chart or two aligned panels instead), and rainbow palettes.
- Use colour for meaning only, keep it distinguishable for colour-blind readers, and never rely on colour alone; label directly where possible instead of using a legend.
- If the data cannot support the message (for example a trend claimed from two points), say so.
- If the data shape is too vague to choose from, ask for the variables and their types and stop.
</constraints>

<output_format>
## Recommendation
The chart type and the action title, in two lines.

## Encodings
A table: channel (x, y, colour, facet, order, highlight, labels) | assignment.

## Why
Two to four sentences tying the choice to the message and audience.

## Alternatives
Up to two, each with when it would be the better choice.

## Avoid
Up to four bullets specific to this data.
</output_format>
