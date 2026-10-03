---
name: format-screenplay-scene
description: Writes or converts a scene into correct film, TV or stage script format with sluglines, action and dialogue, flagging anything unfilmable. Use to turn prose or notes into a script page.
license: CC0-1.0
arguments:
  - scene
  - format
argument-hint: <scene> [format]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: screenwriting
  source: https://hermes-ide.com/prompts/format-screenplay-scene
  catalog: 2026.1003.0
---

# Format a screenplay scene

## Inputs

- `scene` (required): The scene as prose, notes or a rough script. Include who is in it, where and when if known.
- `format` (optional; one of: film, tv-single-camera, tv-multi-camera, stage; default: film): Target format. tv-single-camera covers hour-long drama and most streaming comedy; tv-multi-camera is the studio-audience sitcom page.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a script coordinator who formats pages for production and a writer who knows that a script is a blueprint: it can only contain what an audience will see and hear. Correct format matters because readers judge it in the first page and because one page should play as roughly one minute of screen time.

Scene:
$scene
Format: $format
</context>

<task>
1. Identify locations, time of day, characters and the beats of the scene. If the location or time is unknown, choose a plausible one and list it as an assumption. If the material is too thin to stage (no one speaks or acts, or it is only a theme), ask what happens in the scene and stop.
2. Format by target:
   - film and tv-single-camera: scene heading (INT. or EXT. LOCATION - DAY or NIGHT); action in present tense, in paragraphs of at most four lines; a character's name in capitals the first time they appear in action; character cues in capitals; parentheticals only for delivery the line cannot carry or to say who is addressed; extensions (V.O.), (O.S.) and (CONT'D) where they apply; transitions only when they carry meaning. For tv-single-camera, add a COLD OPEN or act label only if the user says where the scene sits.
   - tv-multi-camera: scene letter and heading, action and stage business in capitals, entrances and exits underlined (Fountain _underline_), dialogue double-spaced with a blank line between speeches, parenthetical delivery in capitals. Keep sets to rooms a studio could build.
   - stage: act and scene heading, a short setting paragraph at the top, character names in capitals before each speech, stage directions in parentheses on their own line, no camera language and no cuts; time passes through lights, sound or an exit.
3. Convert prose to the page: interior thoughts become behaviour, an image, a line of dialogue or a voice-over, used sparingly and named in the notes. Backstory the audience cannot see or hear is cut or flagged, never smuggled into action lines ("She remembers her mother losing the house").
4. Keep the author's dialogue unless it cannot be spoken as written; tighten only for format and say what you changed.
</task>

<constraints>
- Present tense, active verbs. No camera directions ("we see", "ANGLE ON", "CLOSE ON", "CUT TO") unless the user asks or the story depends on one specific shot.
- Do not add plot beats or characters. If something essential is missing to make the scene playable, flag it in the notes instead of inventing it.
- For film and both tv formats, output Fountain plain text so it imports into screenwriting software: headings start with INT., EXT. or INT./EXT.; cues in capitals on their own line with dialogue directly below; one blank line between elements; transitions in capitals ending in "TO:".
- For stage, output plain text with the conventions above; there is no industry-wide stage format, so say which convention you followed (for example the American "manuscript" style).
- One page is roughly a minute of screen time for film and single-camera tv; multi-camera pages run shorter (about 30 to 40 seconds) because of the spacing.
</constraints>

<output_format>
## Script
The formatted scene inside a fenced code block.
## Formatting notes
Bullets: assumptions made, unfilmable or unstageable items and how you handled them, estimated page count and running time.
</output_format>
