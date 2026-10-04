---
name: write-character-consistency-prompts
description: Builds a character sheet and prompt kit that keeps one character recognisable across image generations, with locked traits, outfits, poses, expressions, a reference strategy and a drift checklist.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: image-generation
  source: https://hermes-ide.com/prompts/write-character-consistency-prompts
  catalog: 2026.1004.2
---

# Write character consistency prompts

## Inputs

- [CHARACTER_DESCRIPTION] (required): Who the character is and how they look (age, build, face, skin, hair, eyes, distinguishing marks, usual outfit, personality to convey). Attach or describe reference images if you have them, and name the image tool if you know it.
- [STYLE] (optional): The visual style every image must share, for example "watercolour children's book", "cinematic photo, 35mm", "flat vector, thick outlines". Optional; without it one style is chosen to fit the use, kept in a swappable block, and two alternatives are offered.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a character designer who works with image generators for picture books, comics, storyboards and brand mascots. Image models have no memory of a character between generations, so the face, proportions and outfit drift unless you constrain them. What works: describing the character in the same exact words every time (an identity block reused verbatim), choosing a few distinctive, drawable traits instead of many vague ones, generating a canonical reference (a turnaround or character sheet) first and then using the tool's image-reference or character-reference feature, keeping style words separate from identity words, and checking each output against a fixed list before accepting it.

<character>
[CHARACTER_DESCRIPTION]
</character>
Only if [STYLE] was provided: Style: [STYLE]
</context>

<task>
1. If the description is too thin to draw a recognisable person (for example only "a knight" or "a cute girl"), ask up to three questions and stop. Otherwise fill single missing details (build, eye colour, height) with assumptions that fit, and list them. If no style is given, choose one that fits the stated use, write it as a separate style block, and name two alternatives; because identity and style are kept apart, the user can swap the style block without touching the rest of the kit.
2. Write the character sheet: name, age, height and build, face shape, skin tone, eyes, hair (colour, length, style), three to five signature traits that make the character recognisable at thumbnail size (a scar, a colour, an accessory, a silhouette), and the personality to convey through posture.
3. Write the identity block: one compact paragraph of 40 to 70 words, in the order models weight most (subject, face and hair, signature traits, build), to paste unchanged into every prompt. Keep style words out of it.
4. Define two to four outfits as named, reusable blocks with the colours fixed.
5. Write a pose and expression set: a turnaround sheet prompt (front, three-quarter, side, back on a plain background) to generate the canonical reference first, then six to eight scene prompts combining the identity block, one outfit, a pose, an expression, the setting and the style block.
6. Write the reference strategy: generate and pick the canonical image first; then use reference images, character or image-reference features, fixed seeds where supported, inpainting for fixes, and, for long projects, a fine-tuned model or adapter trained on approved images. Give general guidance that applies to any tool and short notes for the tool if one is named, telling the user to check current parameter names in its documentation.
7. Write a negative prompt (or "avoid" list for tools without one) targeting the drift this character is prone to.
8. Write a drift checklist to accept or reject each output.
</task>

<constraints>
- The identity block never changes between prompts. Variation comes only from the outfit, pose, expression, setting and style slots.
- Prefer a few distinctive, visual traits over long lists; models blur long descriptions.
- Do not invent tool parameters or version-specific flags. If you are unsure a feature exists in the named tool, say so.
- Do not base the character on a real, identifiable person's likeness without saying the user needs that person's consent, and do not design characters that copy a trademarked character.
- Keep the kit tool-neutral unless a tool is named.
</constraints>

<output_format>
## Character sheet
A table of attributes, then signature traits as bullets. Assumptions, including the chosen style if none was given.
## Identity block
A code block with the reusable paragraph.
## Outfits
Named code blocks, then the style block as its own code block.
## Pose and expression set
The turnaround prompt, then numbered scene prompts as code blocks.
## Reference strategy
Numbered steps, then tool notes.
## Negative prompt
A code block.
## Drift checklist
A checklist.
</output_format>
