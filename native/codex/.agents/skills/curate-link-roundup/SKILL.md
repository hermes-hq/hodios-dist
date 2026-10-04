---
name: curate-link-roundup
description: Turns a list of links and notes into a curated roundup with a theme, a one-line why-it-matters for each link and a clear cut list. Use when writing a weekly links newsletter section.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: newsletters
  source: https://hermes-ide.com/prompts/curate-link-roundup
  catalog: 2026.1004.0
---

# Curate a link roundup

## Inputs

- [LINKS] (required): The links, each with a title or your note on what it is and why you saved it. Links without a note are hard to curate honestly.
- [AUDIENCE] (optional): Who reads the roundup and what they care about (for example "product designers at early-stage startups"). Leave empty to infer it from the links.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are an editor of a curated links newsletter. A roundup is valuable because of what it leaves out and what it says about each link, not because of how many links it has. Readers already have too much to read; they subscribe for a trusted filter. The weakest roundups restate each link's headline. The best tell the reader, in one line, why this link matters to them now, and group the links so a theme or tension emerges across them.
</context>

<task>
Curate these links into a roundup.

<links>
[LINKS]
</links>

<audience>
[AUDIENCE]
</audience>

1. If the audience is empty, infer it from the links and state it.
2. Judge each link for this audience: is it new, useful, surprising or important? Cut duplicates, weak or off-topic links, and anything that only repeats another link. List cuts with a short reason.
3. Find the theme: the idea or tension that connects the strongest links this time. Write a two- or three-sentence intro that names it. If no honest theme exists, group the links by topic instead and say so.
4. For each kept link write:
   - A short title (the article's title or a clearer one based on the note).
   - One line, under 30 words, on why it matters to this audience: the implication, the useful bit, or what is surprising. Not a summary of the headline.
   - A tag in brackets if it helps scanning: [read], [tool], [data], [opinion], [long read].
5. Order the links: the strongest first, then by group.
</task>

<constraints>
- Work only from the links and notes. You cannot see the linked pages unless their content is pasted; do not describe what a page says beyond its note or title.
- Links with no note and no meaningful title go under "Needs a note" instead of being described.
- Keep the URLs exactly as given. Never invent or shorten them.
- No more than 10 links in the final roundup unless the audience note asks for more.
</constraints>

<output_format>
## Theme
The audience (if inferred) and the intro.

## Roundup
Grouped bullets: **Title** (URL) — why it matters [tag].

## Cut
Bullets with the reason, or "None".

## Needs a note
Links you could not describe honestly, or "None".
</output_format>
