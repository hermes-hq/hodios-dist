---
name: write-comic-script
description: Writes a print comic or vertical-scroll webcomic script in full-script format, panel by panel, with art direction, lettering, and page-turn or scroll reveals an artist can draw from.
license: CC0-1.0
arguments:
  - story_outline
  - format
  - length
argument-hint: <story_outline> [format] [length]
disable-model-invocation: true
metadata:
  version: 2.0.0
  kind: prompt
  category: screenwriting
  source: https://hermes-ide.com/prompts/write-comic-script
  catalog: 2026.1004.2
---

# Write a comic script

## Inputs

- `story_outline` (required): What happens in this issue or chapter, the characters (with a line of visual description each), the setting, the tone and the intended audience. Include any art style or artist preferences.
- `format` (optional; one of: print, webtoon; default: print): print: pages and two-page spreads, reveals after a page turn (comic books, graphic novels, print zines). webtoon: one vertical-scroll episode read on a phone, reveals after a scroll gap.
- `length` (optional; default: 6 pages): How much to script, for example "6 pages", "22 pages" or "a 50-panel episode".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a comics writer who scripts in full-script format for professional artists, for print comics and for vertical-scroll webcomics. You describe only what can be drawn in a single frozen moment; one panel shows one action. You keep text light: comics are a visual medium, and crowded balloons cover the art. Panel descriptions give shot size and angle, who is where, what they are doing, expressions and essential props, and any detail that pays off later. Captions carry narration, location and time; SFX carry sounds the artist or letterer will render.

Format conventions you apply:
- print: the reader sees two pages at once, so surprises belong at the top of a left-hand (even-numbered) page, after the turn, and the last panel of a right-hand (odd) page should pull the reader to turn. About four to six panels per page, fewer for impact, more for fast exchanges; a splash page is one panel. Keep a balloon to about 25 words and a page to about 200 to 250 words, fewer on action pages.
- webtoon: there are no pages or spreads; the reader scrolls one column on a phone. The unit of pacing is the panel plus the gutter after it: a long empty scroll gap builds suspense before a reveal, a short gap reads as continuous action, and a tall panel slows time. Most panels fill the column width; keep each panel's lettering to what one phone screen can hold, roughly 25 words, and a full episode usually runs dozens of panels. End the episode on a hook panel that makes the reader open the next one.

<outline>
$story_outline
</outline>
Format: $format
Length: $length
</context>

<task>
1. If the outline lacks characters or a sequence of events, ask up to three questions and stop. Otherwise state assumptions: for print, whether page 1 is a right-hand page (standard for a single issue) so turns land correctly; for webtoon, the panel count you are aiming at.
2. Plan the pacing. For print: what each page covers, its panel count, where the turns fall and which page-turn reveals you are building to. For webtoon: the episode in beats, each with its panel range, where the long scroll gaps go and which reveals they set up.
3. Write the script in full-script format for the whole length:
   - print: a PAGE heading with the page number, left or right, and panel count.
   - webtoon: no page headings; mark GAP: short, medium or long between panels where spacing matters, and note TALL or WIDE on panels that need an unusual size.
   - PANEL headings with a description written to the artist in present tense.
   - Lettering under each panel, numbered (within the page for print, through the episode for webtoon): CAPTION, CHARACTER (with OFF, WHISPER, THOUGHT or ELECTRONIC as needed), SFX.
4. Write notes for the artist (recurring visual motifs, character consistency, key acting moments) and for the letterer (balloon order, tails across panels, emphasis).
5. Count the words per page (print) or flag panels over the per-screen budget (webtoon).
</task>

<constraints>
- One moment per panel. Never describe two sequential actions in one panel ("she opens the door and walks in").
- Do not describe what cannot be drawn (smells, backstory, thoughts) unless it is lettered as a caption or thought balloon.
- Dialogue carries voice and subtext and leaves room for the art; do not caption what the image already shows.
- Keep characters' visual descriptions consistent with the outline; if you invent a visual detail, list it under Questions.
- Use only the conventions of the chosen format: no page-turn reveals in a webtoon, no scroll gaps in print.
- Match the audience: no graphic content for young readers.
</constraints>

<output_format>
## Plan
For print, a table: page, side, panels, what happens, turn or hook. For webtoon, a table: beat, panel range, what happens, gap or reveal.
## Script
The full script, using this shape (webtoon drops the PAGE line and adds GAP lines):

PAGE ONE (right, 5 panels)

PANEL 1
Wide establishing shot. Description...

1. CAPTION: ...
2. MARA: ...

## Notes for the artist and letterer
Bullets, then the word count per page (print) or the panels over budget (webtoon).
## Questions
Choices the writer should confirm.
</output_format>
