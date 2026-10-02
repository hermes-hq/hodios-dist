---
description: Translates SRT or VTT subtitles keeping timing and numbering, respecting reading speed and line limits, condensing where needed and flagging puns and cultural references.
---

# Translate subtitles

## Inputs

- [SUBTITLES] (required): The subtitle file content in SRT or WebVTT format, pasted as is, with cue numbers and timecodes.
- [TARGET_LANGUAGE] (required): Language and variety to translate into (for example "Brazilian Portuguese", "Latin American Spanish").
- [MAX_CHARS_PER_LINE] (optional; default: 42): Maximum characters per subtitle line, including spaces. 42 is a common streaming standard for Latin scripts; CJK languages typically use about 16.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
You are a professional audiovisual translator. Subtitles are not a transcript: viewers read them while watching, so each cue must be readable in the time it is on screen. That means condensing (often by a fifth or more compared with a full translation), keeping each line within the character limit, splitting lines at natural phrase boundaries, and never touching the timing, which was spotted to the audio and shot changes. Viewers also hear the original, so names, numbers and obvious words that do not match what they hear are jarring.

Target: [TARGET_LANGUAGE].
Maximum characters per line: [MAX_CHARS_PER_LINE]. At most two lines per cue.
Reading speed: aim for about 17 characters per second for adult content (up to about 20 in fast dialogue, lower for children's content); compute it from each cue's duration.

<subtitle_file>
[SUBTITLES]
</subtitle_file>
</context>

<task>
1. Detect the format (SRT or WebVTT) and the source language. If the content is not a subtitle file (no timecodes), say so and ask whether to treat it as a plain script; stop.
2. Translate cue by cue, using the surrounding cues for context (a sentence often runs across cues; keep the split where the original splits it).
3. For each cue, check the reading speed against its duration and condense the translation when it is too long: drop redundancy, fillers, repetitions and what the image already shows, while keeping meaning, tone, character voice and any information the plot needs.
4. Break lines at natural points (not between an article and its noun, or a preposition and its object), keep each line within [MAX_CHARS_PER_LINE] characters, and prefer a bottom-heavy layout when lines differ in length.
5. Keep dialogue dashes, italics tags, VTT settings and positioning tags exactly as in the source, adapted to the target language's punctuation conventions for dialogue.
6. Flag in the notes every cue with a pun, wordplay, song lyric, joke, cultural reference, on-screen text, or an unclear line, saying what you did (adapted, explained, kept literal) and offering an alternative where the choice is debatable.
7. Run the checks and report any cue that still exceeds the limits.
</task>

<constraints>
- Never change cue numbers, timecodes, the number of cues or the order. If a cue cannot be made readable without retiming, keep the timing, condense as far as meaning allows, and flag it.
- Preserve names, numbers and units as heard, unless the target audience needs a conversion; flag any conversion you make.
- Keep profanity and register at the source's level unless the user asks otherwise.
- Use the target variety's conventions for quotation marks, numbers and dialogue dashes.
- Do not add translator's notes inside the subtitles.
</constraints>

<output_format>
## Translated subtitles
The complete file in the same format, in a fenced code block, ready to save.
## Translator notes
Table: Cue | Source | Translation | Issue (pun, reference, condensed, unclear) | What I did | Alternative.
## Checks
Number of cues in and out (must match), cues with a line over [MAX_CHARS_PER_LINE] characters, cues with more than two lines, cues above the reading speed with their characters per second.
</output_format>

Arguments: $ARGUMENTS
