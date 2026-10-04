---
name: critique-graphic-design
description: Gives structured, prioritised feedback on a poster, social graphic, slide or layout covering purpose, hierarchy, typography, colour, composition and production. Use before finalising a design.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: graphic-design
  source: https://hermes-ide.com/prompts/critique-graphic-design
  catalog: 2026.1004.1
---

# Critique a graphic design

## Inputs

- [DESIGN] (required): An image of the design, or a precise description of its elements, sizes, colours, fonts and placement. Include the format and size (e.g. A2 poster, 1080 x 1350 feed post).
- [PURPOSE] (optional): What the design must achieve, for whom, and where it will be seen. Optional; without it the purpose is inferred and stated.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Useful design feedback is specific, tied to the purpose, and ordered: the one change that fixes the read from three metres away matters more than a kerning pair. Unhelpful feedback is taste ("I don't love the green"), vague ("make it pop"), or a rewrite of the designer's style. The critic's job is to say whether the piece communicates, to whom, in its real viewing context, and what would make it communicate better.
</context>

<task>
Critique this design.

<design>
[DESIGN]
</design>
Only if [PURPOSE] was provided: 
<purpose>
[PURPOSE]
</purpose>

1. State the purpose, the audience and the viewing context (distance, time spent, screen or print). If not given, infer them and say so.
2. **Read test:** describe the order in which the eye moves through the piece, and whether the one thing the viewer must take away is read first. For posters, judge the read at a distance; for feeds, at thumbnail size in under two seconds.
3. Review, noting only what matters:
   - **Hierarchy:** a clear entry point, contrast of size, weight and colour between levels, and how many competing focal points there are.
   - **Typography:** typeface fit and number of families, size steps, line length and leading, alignment and rag, tracking, widows and orphans, and legibility at the viewing size.
   - **Colour:** contrast between text and background (judge large-text and small-text legibility separately), harmony, brand fit, and meaning carried by colour alone.
   - **Composition:** grid, alignment, balance, white space, edges and margins, image cropping, and the path the eye takes.
   - **Imagery and copy:** do image and words reinforce each other, and is the copy as short as it can be?
4. For each point, give the observation, why it matters for the purpose, and a concrete change. Prioritise as **must fix** (hurts the message), **should fix** (weakens it) or **consider** (refinement).
5. **Production checks** for the medium: print (bleed, safe margins, resolution of at least 300 ppi at final size, CMYK or spot colours, minimum type size, rich black) or screen (platform safe zones and crops, text legibility on mobile, file size and format).
6. Describe the next version in a few lines: what changes, and what stays.
</task>

<constraints>
- Separate taste from function. Label anything that is taste as "taste" and never mark it must fix.
- Respect the designer's style; suggest changes within it unless the style itself works against the purpose.
- When working from a description, mark judgements that depend on details you cannot see. Do not state exact contrast ratios unless you have exact colours.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
2 sentences: does it work for its purpose, and the single most important change.
## What works
Up to 4 bullets, specific.
## Feedback
| Priority | Area | Observation | Why it matters | Change |
## Production checks
Checklist for the medium, each marked ok, issue or unknown.
## Next version
</output_format>
