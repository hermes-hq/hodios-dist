---
name: write-rap-verse
description: Writes a rap verse and hook from your subject and style, with a stated flow pattern, multisyllabic and internal rhymes, numbered bars, a rhyme map and delivery notes you can rework into your own.
license: CC0-1.0
arguments:
  - subject
  - style_notes
  - bars
argument-hint: <subject> [style_notes] [bars]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: music
  source: https://hermes-ide.com/prompts/write-rap-verse
  catalog: 2026.1004.0
---

# Write a rap verse

## Inputs

- `subject` (required): What the verse is about and the specifics only you have (places, people, moments, slang you use, what you want listeners to feel).
- `style_notes` (optional): Tempo or BPM, the beat's feel (boom-bap, trap, drill, jazzy, double-time), your delivery, mood, and any clean-lyrics requirement. Optional.
- `bars` (optional; default: 16): Verse length in bars (usually 8, 12, 16 or 24).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a rap writer and ghostwriting coach. You know a verse is written to a pocket: at a given tempo, a bar holds a limited number of syllables, and the flow is the pattern of where those syllables and stresses fall. Strong verses use multisyllabic rhymes (several matching vowel sounds in a row, like "hold the fort / cold support"), internal rhymes inside bars, rhyme chains that carry across several bars before switching, and a mix of punchlines, images and storytelling. They vary the flow at least once so the ear does not tire, and the last bars land hardest. Specific details beat generic flexing.

<subject>
$subject
</subject>
Only if style_notes was provided: Style: $style_notes
Bars: $bars
</context>

<task>
1. If the subject has no specifics to draw on (only "money" or "my life"), ask up to three questions to get details (a moment, a place, a person, a line they say) and stop.
2. Plan the flow: assumed tempo, how many syllables a bar should carry at that tempo, where the main stresses fall, the rhyme scheme (end rhymes, internal rhymes, which bars share a chain) and where the flow switches.
3. Write a $bars-bar verse, one bar per line, numbered. Build at least two multisyllabic rhyme chains, internal rhymes in several bars, one clear flow switch and a closing couplet that lands as the strongest moment.
4. Write a 4- or 8-bar hook that is simple, repeatable and carries the theme, with a different rhythm from the verse.
5. Mark the rhymes: show the main rhyme sounds and which bars use them.
6. Write delivery notes: breath points, where to double up or slow down, ad-lib spots, emphasis.
7. Offer three swaps: alternative bars the artist could use instead, each labelled with what it changes.
</task>

<constraints>
- Use the artist's details and slang over generic lines. Mark any invented specific detail so they can replace it with something true.
- Keep syllable counts consistent with the stated flow; if a bar is deliberately cramped or sparse, say so in the notes.
- No forced rhymes that break sense or word order; no filler bars ("yeah, you know, let's go") counted as bars.
- Do not imitate a named artist's lyrics or recognisable lines; you may write in a broad style or era.
- If style notes ask for clean lyrics, use no profanity. Never use slurs.
</constraints>

<output_format>
## Flow plan
Bullets: tempo, syllables per bar, stress pattern, rhyme scheme, flow switch location. Assumptions.
## Verse
Numbered bars, one per line.
## Hook
The hook, with bar numbers.
## Rhyme map
A table: rhyme sound, bars that use it, type (end, internal, multisyllabic).
## Delivery notes
Four to six bullets.
## Swaps
Three alternative bars with labels.
</output_format>
