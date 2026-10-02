---
name: write-plotting-code
description: Writes publication-quality plotting code from data and intent, with labelled axes, accessible colours and an annotation on the key point. Use for matplotlib, seaborn, plotly, ggplot2 or Vega-Lite.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: data-visualization
  source: https://hermes-ide.com/prompts/write-plotting-code
  catalog: 2026.1002.0
---

# Write plotting code

## Inputs

- [DATA] (required): The data (a small table pasted inline) or its structure (file or dataframe name, columns and types, a few sample rows).
- [INTENT] (required): What the chart should show and the key point to annotate, plus the output target (slide, paper, web) and size if it matters.
- [LIBRARY] (optional; one of: matplotlib, seaborn, plotly, ggplot2, vega-lite; default: matplotlib): Plotting library to write the code for.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write plotting code the way a good data journalist builds charts: the default output of a plotting library is a starting point, not a finished chart. A finished chart has a title that states the point, labelled axes with units, no chart junk, colours that survive colour-blindness and greyscale printing, direct labels instead of a legend where possible, and one annotation that points at the thing the reader should see.
</context>

<task>
Write [LIBRARY] code for this chart.

<data>
[DATA]
</data>

<intent>
[INTENT]
</intent>

1. Choose the chart type that best serves the intent, in one sentence. If the intent asks for a type that will mislead (for example a truncated bar chart or a pie with many slices), use a better one and say why.
2. Write complete, runnable code: imports, data loading (inline data if given, otherwise a clearly named file or dataframe placeholder matching the described columns), any reshaping, the plot, and saving to a file (PNG at 200 dpi or more and SVG for matplotlib, seaborn and ggplot2; HTML for plotly; a valid JSON spec for Vega-Lite).
3. Apply these defaults unless the intent says otherwise:
   - An action title stating the point, a subtitle with units and period, and a source or note line.
   - Axis labels with units; thousands separators, percentages and dates formatted for reading.
   - Bars starting at zero; sorted categories when order is not inherent.
   - A colour-blind-safe palette (Okabe-Ito or viridis for sequential data); the key series in one strong colour and the rest in grey.
   - Direct labels at line ends or on bars instead of a legend when there are five or fewer series.
   - Minimal gridlines, no top and right spines, no 3D or shadows.
   - One annotation (text plus an arrow or marker) at the key point named in the intent.
4. Keep the code readable: constants for colours and sizes at the top, short comments for non-obvious choices.
</task>

<constraints>
- Use only the chosen library and its normal companions (pandas or numpy for Python libraries, the tidyverse and scales for ggplot2). No custom fonts or files that may not exist; if a style choice needs one, make it optional.
- Do not invent data. If the data is described but not given, write code that reads it, with the expected columns named. If key columns needed for the intent are missing, ask for them and stop.
- The annotation must be computed from the data where possible (for example the maximum, or the last point), not hard-coded coordinates, so the chart stays right when data updates.
- Make the figure size suit the target: wide for slides, column width for papers, responsive for web.
</constraints>

<output_format>
## Chart choice
One or two sentences.

## Code
One complete code block.

## Notes
Up to four bullets: how to adapt it (other series to highlight, size for another target), and anything assumed about the data.
</output_format>
