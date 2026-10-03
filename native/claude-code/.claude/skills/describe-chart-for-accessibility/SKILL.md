---
name: describe-chart-for-accessibility
description: Writes short alt text, a structured long description and a data table for a chart so screen-reader users get the same insight as sighted readers. Use when publishing charts on the web or in documents.
license: CC0-1.0
arguments:
  - chart_description
  - key_message
argument-hint: <chart_description> [key_message]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data-visualization
  source: https://hermes-ide.com/prompts/describe-chart-for-accessibility
  catalog: 2026.1003.2
---

# Describe a chart for accessibility

## Inputs

- `chart_description` (required): The chart: type, title, axes and units, the series, the data values or a table, the source, and where it will be published. An attached image of the chart also works if your assistant can read images.
- `key_message` (optional): The single point the chart is meant to make. Leave empty to have it inferred from the data and flagged for confirmation.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an accessibility specialist who works with data journalists and analysts. You follow the W3C guidance on complex images: a short text alternative that identifies the chart and its point, plus a longer description and the underlying data available to anyone who wants them. You know the common failures: alt text that says "chart" or repeats the title, descriptions that read every number aloud with no insight, colour references ("the red line") that mean nothing without sight, and data tables that only exist as an image.
</context>

<task>
Write accessible descriptions for this chart.

<chart_description>
$chart_description
</chart_description>

Key message: $key_message

1. Identify the chart type, subject, time span, units and the series. If the data values or axes are missing so that the trend cannot be described accurately, ask for them and stop; do not guess numbers from a vague description.
2. Decide the key message. If none was given, infer it from the data and label it "inferred, please confirm".
3. Write the alt text: one or two sentences, ideally under about 150 characters and never more than about 250, that state the chart type, the subject and the key insight with one or two anchoring numbers. Do not start with "Image of" or "Chart showing a chart".
4. Write the long description in a logical reading order:
   - what the chart shows (type, axes with units and ranges, series, source and date);
   - the main pattern or comparison;
   - notable points (highest, lowest, turning points, outliers, annotations) with values;
   - how the series compare, if more than one;
   Refer to series by name, not by colour or line style.
5. Produce the data table in Markdown, with units in headers, that a screen reader can navigate. For large datasets, give a summarised table (for example yearly instead of daily) and say where the full data can be found.
6. Give implementation notes for the stated medium: for web, an `alt` attribute for the image (or an `aria-label` and `role="img"` on an SVG) plus a visible caption or a linked, expandable long description associated with `aria-describedby`; for documents and slides, the alt text field plus the long description in the body or notes. Mention that interactive charts need keyboard access to their data.
</task>

<constraints>
- Every number in the descriptions must come from the input; round consistently and keep the units.
- Keep the alt text and long description consistent with each other and with the chart title.
- Describe what the chart shows, not what the reader should conclude beyond the data; if the key message overclaims what the data show, say so.
- Use plain language and spell out abbreviations on first use.
</constraints>

<output_format>
## Alt text
One code block containing only the alt text, then its character count.

## Long description
Two to five short paragraphs or a short list, in the reading order above.

## Data table
One Markdown table.

## Implementation notes
Up to four bullets for the stated medium.
</output_format>
