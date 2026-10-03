---
name: define-iconography
description: Defines an icon system with grid and keylines, stroke and corner rules, sizes, naming, metaphors, accessibility and contribution rules. Use when a design system creates or tidies up its icons.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: design-systems
  source: https://hermes-ide.com/prompts/define-iconography
  catalog: 2026.1003.2
---

# Define an icon system

## Inputs

- [BRAND_STYLE] (required): The brand's visual character (typeface, corner radius, line weights, illustration style, adjectives) and any existing icons or icon library in use.
- [ICON_NEEDS] (optional): The concepts and actions the product needs icons for, platforms, and current problems (mixed styles, unclear metaphors, inconsistent sizes). Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Icon sets drift quickly: icons from three libraries mixed together, strokes of 1.5 and 2 pixels side by side, a trash can that means "delete" on one screen and "archive" on another, icons named after what they do in one feature so the same glyph has four names, and icon-only buttons that screen readers announce as "button". An icon system fixes the geometry so every icon looks like part of one family, fixes the meaning so each glyph means one thing, and makes the rules clear enough that a new contributor can draw an icon that fits.
</context>

<task>
Define the icon system.

<brand_style>
[BRAND_STYLE]
</brand_style>
Only if [ICON_NEEDS] was provided: 
<icon_needs>
[ICON_NEEDS]
</icon_needs>

If the brand style is too thin to set construction rules (no typeface, radius, line character or existing icons), ask up to three questions and stop.

1. **Principles.** Three or four principles that follow from the brand (for example "simple enough to read at 16 pixels", "friendly but precise: rounded terminals, geometric forms") and that rule something out.
2. **Grid and keylines.** A base grid (commonly 24 by 24 with 2 units of padding, giving a 20 by 20 live area), keyline shapes (circle, square, portrait and landscape rectangles) so icons of different shapes look the same size, and pixel-snapping rules.
3. **Construction rules.** Stroke weight in grid units and whether it scales with size, stroke caps and joins, corner radius (outer and inner) matched to the brand's UI radius, minimum gap between strokes, how to handle angles (for example multiples of 15 or 45 degrees), filled versus outlined construction, perspective (flat, no 3D), and level of detail.
4. **Sizes and scaling.** The sizes supported (for example 16, 20, 24 and 32), whether smaller sizes get simplified drawings, alignment with text (optical centring with text baseline and line height), and touch-target padding around icon buttons.
5. **Styles and states.** Outlined and filled styles and when each is used (for example filled for the selected state in navigation), colour rules (icons inherit text colour; colour only for status, never as the only signal), and disabled and active states.
6. **Metaphors.** For each concept in the icon needs (or common product concepts if none were given), propose the metaphor, note ambiguity or cultural risk (a floppy disk for save, a mailbox that looks different across countries, hand gestures, religious symbols), and say whether it needs a text label. Mark concepts that should not be icons at all because no metaphor is widely understood. Assign each glyph one meaning only.
7. **Naming.** Name icons by what they depict, not by the action in one feature ("trash", not "delete-project"), in a consistent pattern (for example object then modifier: "arrow-left", "bell-off", "heart-filled"), lowercase kebab case, with a list of aliases for search.
8. **Accessibility.** Decorative icons hidden from assistive technology; meaningful icons and icon-only buttons with an accessible name; visible text labels for important or ambiguous actions; non-text contrast of at least 3:1 against the background for meaningful icons; tooltips that are not the only label; mirroring rules for right-to-left languages (directional icons flip, others such as a clock or media play do not).
9. **Production and contribution.** Source file structure, SVG export rules (single path where possible, no hidden layers, `currentColor` fills, consistent viewBox, no embedded raster), optimisation, versioning, and a contribution checklist for new icons including review steps.
</task>

<constraints>
- Base geometry on the brand description; when you assume a value, say so.
- If the team uses an existing open-source icon library, recommend extending it with its own rules rather than mixing styles, and check its licence terms before modification.
- Do not draw or invent icons as images; describe them precisely enough for a designer.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings. Construction rules as a table:
| Property | Rule | Reason |
Metaphors as a table:
| Concept | Metaphor | Ambiguity or risk | Needs label? | Icon name |
End with the contribution checklist as yes-or-no items.
</output_format>
