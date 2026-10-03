---
name: audit-design-consistency
description: Inventories spacing, type, colour, radii and component variants across screens, finds near-duplicates and plans their consolidation. Use before building or cleaning up a design system.
license: CC0-1.0
arguments:
  - screens
  - design_system
argument-hint: <screens> [design_system]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: design-systems
  source: https://hermes-ide.com/prompts/audit-design-consistency
  catalog: 2026.1003.1
---

# Audit design consistency across screens

## Inputs

- `screens` (required): Screenshots, exported style values (e.g. a CSS or design-file style dump) or descriptions of the screens to audit. Name each screen.
- `design_system` (optional): The current design system or style guide, if any, so values can be checked against it. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Products drift: 14 greys that should be 6, button heights of 36, 38 and 40 px, three ways to show an error, spacing that is "about 16" everywhere. Each difference is small, but together they slow every designer and engineer and make the product feel unreliable. An interface inventory makes the drift visible, separates intentional differences from accidental ones, and turns the clean-up into an ordered plan instead of a big-bang redesign.
</context>

<task>
Audit these screens for consistency.

<screens>
$screens
</screens>
Only if design_system was provided: 
<design_system>
$design_system
</design_system>

1. **Inventory** every distinct value you can identify, per property: colours (text, backgrounds, borders), type (family, size, weight, line height), spacing (padding, gaps, margins), radii, borders, shadows, icon sizes and styles. For each value, record where it appears and how often.
2. **Cluster near-duplicates:** values a user cannot tell apart or that serve the same role (`#6B7280` and `#6B7380`, 15 px and 16 px body text, 7 px and 8 px radius). Propose one canonical value per cluster, preferring the design system's value, then the most frequent one.
3. **Check the scale:** flag values off the spacing and type scale (or, without a design system, propose the scale implied by the most common values, for example a 4 px base).
4. **Component variants:** list each component type (buttons, inputs, cards, alerts, tabs, modals) and every visual or behavioural variant found. Mark each variant keep, merge or remove, and name variants that exist for a real reason.
5. **Intentional versus accidental:** a difference is intentional if it signals a different role or state. Do not merge those; say why they differ.
6. **Consolidation plan:** order the work by impact (frequency times visibility) and risk. Start with tokens for colour and type, then spacing, then components. Group changes so each can ship on its own.
7. If screenshots are low resolution or the description lacks values, report what can be judged visually and say what exact values are needed (for example an exported style list).
</task>

<constraints>
- Report only values present in the input. Do not invent counts; when you can only estimate from images, say "approximately" and mark it.
- Colour values read from screenshots are approximate because of compression and colour profiles. Say so and recommend confirming from source files.
- Do not redesign. The aim is fewer, consistent values, not a new look.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Summary
The size of the drift in numbers (for example "11 text colours for 4 roles") and the top 3 actions.
## Inventory
One table per property: | Value | Where used | Count | Cluster | Verdict (keep / merge into X / remove) |
## Component variants
| Component | Variants found | Keep / merge / remove | Reason |
## Consolidation plan
Numbered phases, each with scope, impact, risk and what to check after.
## Mapping
| Old value | New value or token | Screens affected |
## Questions
</output_format>
