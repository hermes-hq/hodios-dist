---
description: Suggests typeface pairings with rationale, roles, weights, a starter type scale, fallbacks and licensing notes. Use when choosing fonts for a brand, site or publication.
agent: agent
argument-hint: brand_personality medium
---

# Pair typefaces for a brand

<context>
Font-pairing advice is usually a list of famous names with "classic and modern" as the reason. A pairing works when the two faces have a clear job each, differ enough to be distinguishable but share proportions or structure so they sit together, and hold up in the real medium: small sizes on screens, long reading in print, the languages the brand writes in, and the licence the budget allows.
</context>

<task>
Suggest typeface pairings for this brand, for ${input:medium:Where the type will be used, which decides licensing, rendering and performance concerns.}.

<brand_personality>
${input:brand_personality:What the brand is and how it should feel, the audience, and any fonts already in use or ruled out. Mention languages or scripts the text must support.}
</brand_personality>

1. Turn the personality into 3 to 4 typographic traits (for example "warm, humanist, high legibility at small sizes, slightly editorial"), and say which ones are must-haves.
2. Propose 3 to 4 pairings. At least one should be free to use under an open licence, and at least one should be a different structural idea (for example serif plus sans, then sans plus mono, or a superfamily with matching serif and sans). For each pairing give:
   - the faces and their roles (display or headings, body, UI or captions, optional mono or numerals);
   - why they pair: contrast in classification or weight, and shared traits such as x-height, proportions, stroke contrast or construction;
   - the weights and styles actually needed (keep it to the fewest files that cover the roles), and whether a variable version exists;
   - legibility notes for ${input:medium:Where the type will be used, which decides licensing, rendering and performance concerns.}: small-size rendering and hinting on screens, or text colour and paper for print; tabular figures if numbers matter;
   - language and script coverage relevant to the brief;
   - licensing: open licence (such as the SIL Open Font License), subscription service, or commercial foundry licence, and what each covers (desktop, web, app embedding, page views).
3. Recommend one pairing and say why it fits best.
4. Give a starter type scale for the recommended pairing: 5 to 7 steps from caption to display, with sizes, line heights and the face and weight for each. For web, use rem values and a ratio; for print, use points.
5. Give fallbacks: a system font stack for web, or substitutes if the licence is out of budget.
</task>

<constraints>
- Recommend only real, currently available typefaces. If you are not certain a face exists under that exact name, or of its licence terms or language coverage, say "verify" rather than guessing.
- Licensing terms vary by foundry and change. Always tell the user to confirm the licence for their use (web, app, print run, logo) with the foundry or distributor.
- Do not pick fonts on novelty. Legibility at the real sizes comes first.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Brief
The traits, with must-haves marked.
## Pairings
For each: a heading with the pairing, then a table | Role | Typeface | Weights | Notes |, followed by the reason it pairs, the medium notes, coverage and licence.
## Recommendation
## Type scale
| Step | Use | Face and weight | Size | Line height |
## Licensing and delivery
Licences to confirm, fallbacks, and for web, how to load the fonts (self-hosting, subsetting, `font-display`).
</output_format>
