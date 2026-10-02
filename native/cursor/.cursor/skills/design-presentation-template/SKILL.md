---
name: design-presentation-template
description: Specifies a branded presentation template with master layouts, type scale, colour use, chart styles, image rules and do and don't examples. Use when brand or comms teams build a slide template.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: graphic-design
  source: https://hermes-ide.com/prompts/design-presentation-template
  catalog: 2026.1002.2
---

# Specify a presentation template

## Inputs

- [BRAND] (required): The brand assets - logo versions, colour values, fonts (and which are installed on staff computers), imagery style - and how the brand should feel.
- [USE_CASES] (optional): Who builds decks and for what (sales pitches, board updates, all-hands, conference talks, training), the tool (PowerPoint, Google Slides, Keynote) and common problems with current decks. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Company slide templates usually contain a beautiful title slide and an empty content slide, so every presenter improvises: 14-point text, six colours in a pie chart, logos pasted on every slide, stretched photos and fonts that fall back to defaults on someone else's laptop. A template that works is built for the people who will actually fill it, under time pressure, in their tool: a small set of layouts that cover real content, styles that make the right choice the easy one, and rules short enough to remember.
</context>

<task>
Specify a presentation template.

<brand>
[BRAND]
</brand>
Only if [USE_CASES] was provided: 
<use_cases>
[USE_CASES]
</use_cases>

Use only the brand values given. If colour values or fonts are missing, mark them [TBD] and continue; if there is no brand information at all, ask for it and stop.

1. **Template principles.** Three to five rules for presenters (for example "one message per slide, stated in the title", "the brand shows through colour and type, not logos on every slide").
2. **Format and grid.** 16:9 by default (say if a use case needs 4:3 or a portrait format for documents), margins, a column grid, safe areas for projection, and where the title, body, footer, slide number and source line sit.
3. **Master layouts.** Specify 10 to 14 layouts that cover the use cases, for example: title, agenda, section divider, title and body, two columns, big statement or number, chart with takeaway title, table, image with caption, full-bleed image with text, quote, team or people, comparison, and closing. For each: purpose, placeholders and their positions on the grid, and when to use it. Add document-style layouts if decks are sent rather than presented.
4. **Typography.** Font families with fallbacks that are installed or embeddable in the tool named, so decks do not break on other computers; a type scale in points for titles, subtitles, body, captions and footnotes with line spacing; minimum sizes for presented slides (body text no smaller than about 18 points) and for read-only documents; title style as an action title stating the takeaway.
5. **Colour.** The theme colour slots of the tool (background, text, accents) mapped to brand colours, roles and proportions, which combinations are allowed for text, and a chart palette order of 4 to 6 colours plus a highlight colour and a neutral for "everything else".
6. **Charts and tables.** Default chart styles (no 3D, no shadows, light or no gridlines, direct labels instead of legends where possible, one highlighted series), when to use bar, line, stacked and scatter, table styles (alignment of numbers, row shading, header style), and the source line format.
7. **Images and icons.** Photography and illustration style, cropping and placement rules, never stretching or adding effects, image resolution, icon style and sizes, and logo usage (title and closing slides only, unless a rule says otherwise).
8. **Accessibility.** Contrast of text on every background (4.5:1 for body text), reading order set in each layout, alt text for meaningful images, no meaning by colour alone, slide titles unique so navigation works, and captions or notes for embedded video.
9. **Do and don't.** Eight pairs, each describing a concrete slide example.
10. **Build notes.** How to build the template in the tool named: master and layout setup, theme colours and fonts, placeholder types, locked elements, file naming and where the template lives, and a short presenter quick-start of five bullets.
</task>

<constraints>
- Do not invent colour codes, fonts or logo versions.
- Keep the layout set small: every layout must map to a real use case, and say which.
- Tool features differ; only recommend features available in the named tool, and say when something needs a workaround.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings. Master layouts as a table:
| # | Layout | Purpose | Placeholders and positions | Use case |
Type scale as a table: | Style | Font | Size (pt) | Line spacing | Use |
Do and don't as a two-column table.
</output_format>
