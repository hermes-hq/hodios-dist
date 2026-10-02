---
name: write-film-treatment
description: Writes a present-tense treatment for a film or series with title, logline, tone, main characters, the story act by act or the season arc, and the ending. Use when pitching a project.
license: CC0-1.0
arguments:
  - story
  - length
argument-hint: <story> [length]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: screenwriting
  source: https://hermes-ide.com/prompts/write-film-treatment
  catalog: 2026.1002.2
---

# Write a film or series treatment

## Inputs

- `story` (required): The story in any form (notes, an outline, a beat sheet, a draft summary), including the ending. Say whether it is a feature film or a series, and the genre.
- `length` (optional; default: 3 to 5 pages): Target length, e.g. "2 pages", "5 pages", "about 2,500 words". A page is about 400 to 500 words of treatment prose.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A treatment is the story told as vivid prose, in the present tense, so that a producer, executive or financier can see the film or series before the script exists. It is a selling document and a structural test at once: it must read quickly and make the reader feel the tone, and it must show that the story holds together from the inciting incident to an ending that pays off. Treatments fail when they read like a dry list of events, when they hide the ending to create suspense, when they bury the reader in minor characters and subplots, or when they describe camera moves instead of story.
</context>

<task>
Write a treatment for this story.

<story>
$story
</story>

Target length: $length

1. Decide whether this is a feature film or a series. If the story does not say and you cannot tell, or it lacks a protagonist, a central conflict or an ending, ask for what is missing (at most three questions) and stop.
2. **Choices made:** a short list of every gap you filled or decision you made (a character's name, a motive, how a scene resolves), so the writer can accept or change them. Keep invented material to what the story needs.
3. **Treatment for a feature film**, with these headed parts:
   - **Title** and **logline** (one sentence: protagonist, goal, opposition, stakes);
   - **Tone and world:** a short paragraph on genre, tone and visual feel, using the story's own imagery; at most one or two comparable films, described by what is shared;
   - **Main characters:** the protagonist, the antagonist and two or three key supporting characters, two to four sentences each: who they are, what they want, what they hide or fear, and how they change;
   - **Story:** Act One, Act Two (with the midpoint turn), Act Three, told as present-tense prose in story order, emphasising cause and effect, key set pieces and the emotional turns. Give a line or two of dialogue only where it defines a character or a moment;
   - **Ending:** the climax and resolution stated plainly, and what the ending means.
4. **Treatment for a series**, with these headed parts: title and logline; tone and world; the series engine (what generates stories week after week or season after season); main characters with their arcs over the first season; the pilot told in present-tense prose; the season one arc and its finale; and a paragraph on where future seasons could go.
5. Fit the length: spend most words on the story itself, compress the setup, and make the climax as vivid as the opening.
</task>

<constraints>
- Present tense, third person, prose paragraphs. No scene headings, camera directions, shot lists or screenplay formatting.
- Reveal the ending. Do not end on a cliffhanger or a question.
- Introduce characters in capitals the first time they appear in the story section, with an age and a one-line description.
- Name only characters who matter to the main story; refer to others by role ("her landlord").
- Keep the writer's plot, characters and ending; flag any change you think would help in Choices made instead of making it silently.
</constraints>

<output_format>
## Choices made
A short list, or "None".
## Treatment
The treatment with the headed parts above, as continuous prose under each heading.
</output_format>
