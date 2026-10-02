---
name: songwriting-track
description: Takes a song from concept and title to hook, verse lyrics, structure, a chord sketch and a final edit, pausing for the songwriter between steps. Use when writing a complete song.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: music
  source: https://hermes-ide.com/prompts/songwriting-track
  catalog: 2026.1002.2
---

# Songwriting track

## Inputs

- [CONCEPT] (required): What the song is about, in any form (a situation, a feeling, a title, a line you love, a story). Concrete details help.
- [GENRE] (optional): The genre or sound, e.g. "indie folk", "90s R&B", "country", "pop-punk". Optional; step 1 asks if missing.
- [MOOD] (optional): The feeling the listener should be left with, e.g. "bittersweet", "defiant", "giddy". Optional; step 1 asks if missing.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Writes a complete song with the songwriter, the way a good co-write runs: idea and title, chorus hook, verses that earn it, structure and chords, then a line edit.

<concept>
[CONCEPT]
</concept>

Genre: [GENRE]. Mood: [MOOD]. If either is blank, step 1 asks for it.

Rules for every step:
- The songwriter owns the song. Offer options and ask for decisions on anything that defines it (title, point of view, story, genre, the last line) instead of choosing silently.
- Build on the approved documents. Never change an approved title, hook or line without flagging it and saying why.
- Write for singing: natural word stress on strong beats, matched syllable counts between parallel lines, open vowels on held notes, no word order bent for a rhyme.
- Write original lyrics. Do not reproduce or lightly alter existing songs; for "in the style of" requests, capture general traits (themes, imagery, rhyme habits, structure) without copying lines.
- Keep each document short, and do not write sections a later step owns.
- If the songwriter wants to go faster, offer a fast route (one question per step, shorter documents) but keep every approval gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. concept (discover)
2. hook (design)
3. verses (build)
4. structure (build)
5. final-edit (review)

### Step 1: Concept and title

Turn the concept into a song idea specific enough to write.

1. Ask, in one message, only what you cannot infer: the genre and mood if not given; who is singing to whom (point of view); whether there is a melody, a line or a title already; any detail that must stay; and where the song is for (a release, a gift, practice, a specific artist to pitch to).
2. Once answered, state the idea in one sentence: the situation, the emotional turn, and the one feeling the listener should leave with.
3. Offer three distinct angles on it, each with: a working title that could be the hook (short, singable, a phrase people say or could say); the point of view; the central image or object that carries the emotion; and how the title's meaning could shift by the last chorus.
4. For each angle, name its risk in one line (too familiar, too abstract, hard to sing, too narrow).
5. Recommend one angle and say why, or a merge of two.

Write the document with sections Answers, The idea, Angles, Recommendation.

Stop and wait for the songwriter to choose a title and angle.

Save this step's result to `song-notes/01-concept.md`.

**Gate:** stop here and wait for the user's approval before step 2 (hook).

### Step 2: Hook and chorus

Write the chorus first, because every other section exists to set it up.

1. Restate the approved title and angle in one line.
2. Write two or three chorus options. Each one:
   - puts the title on the first line, the last line, or both;
   - states the song's core idea plainly enough to sing along to, while keeping one concrete image;
   - has a clear rhyme scheme (often AABB or ABAB in pop and country; looser in indie and hip-hop) and lines short enough to repeat;
   - fits the approved genre's chorus length (usually four to eight lines).
3. Under each option give: the rhyme scheme, syllable count per line, the stressed syllables in the title line, and where the long held notes are likely to fall (open vowels there).
4. If the songwriter has a melody, ask for its rhythm (syllables per line, where the long notes are) and fit the words to it instead of inventing a new rhythm.
5. Suggest a post-chorus or tag line only if the genre uses one.

Write the document with sections Title, Chorus options, Prosody notes.

Stop and wait for the songwriter to pick or adjust a chorus. Ask which line they would sing first.

Save this step's result to `song-notes/02-hook.md`.

**Gate:** stop here and wait for the user's approval before step 3 (verses).

### Step 3: Verses and pre-chorus

Write verses that earn the approved chorus.

1. Plan the story across the verses in one line each: verse 1 sets the scene (who, where, what just happened); verse 2 moves time forward or deepens the stakes, with new information and never the same story in other words; any later verse lands the turn.
2. Write verse 1 and verse 2 with concrete, sensory detail (objects, places, actions, a line of speech) instead of naming emotions. Keep parallel lines within one or two syllables of each other so one melody can carry both verses, and keep the same rhyme scheme in both.
3. If the genre uses one, write a pre-chorus that lifts toward the chorus: shorter lines or a change of rhythm, rising tension, and a last line that leads straight into the title.
4. Mark the two lines you are least sure of and give one alternative for each.
5. Check every line against the chorus: does it point toward it, and does it make the title hit harder the second time?

Write the document with sections Story map, Verse 1, Pre-chorus, Verse 2, Weak spots.

Stop and wait for the songwriter's reaction before arranging the song.

Save this step's result to `song-notes/03-verses.md`.

**Gate:** stop here and wait for the user's approval before step 4 (structure).

### Step 4: Structure and chord sketch

Assemble the approved sections into a song and sketch the harmony.

1. Propose a section order suited to the genre with an approximate bar count per section. Say how long the song runs at the suggested tempo, and how soon the first chorus arrives.
2. Write the bridge, if the structure has one: a new angle on the idea (a confession, a flash forward, the other person's side, a reversal), different in line length and rhythm from the verses, leading back into the last chorus. Suggest whether the last chorus repeats exactly or changes one deliberate line.
3. Sketch chords per section in a singable key for a typical voice in the genre, with Roman numerals beside the chord names (for example "G D Em C = I V vi IV") so the songwriter can transpose. Give the verse, pre-chorus, chorus and bridge different harmonic colour: for example start the chorus on the I chord after a pre-chorus that ends on V or IV, or move the bridge to the vi or IV.
4. Add a dynamics map: where the song is sparse, where it builds, where it peaks and where it drops out.
5. Note that the chord sketch is a starting point; the melody may need different chords under specific words.

Write the document with sections Song map, Bridge, Chord sketch, Dynamics.

Stop and wait for the songwriter to approve the structure before the final edit.

Save this step's result to `song-notes/04-structure-and-chords.md`.

**Gate:** stop here and wait for the user's approval before step 5 (final-edit).

### Step 5: Final edit

Polish the whole lyric without changing what the songwriter approved.

1. Assemble the full lyric in the approved order with section labels in square brackets ([Verse 1], [Chorus], [Bridge]) and chord names above the first line of each section.
2. Edit line by line for: cliché and stock phrases; abstract emotion words where an image would work; forced rhymes and bent word order; stress landing on weak syllables; parallel lines whose syllable counts drift apart; repeated words that are not deliberate; and lines that say what an earlier line already said.
3. For each change, show the original line, the suggested line and the reason, in a table. Change nothing silently. Keep the title, the hook and any line the songwriter marked as fixed exactly as approved.
4. Run a final check and report it: the title appears in every chorus; verse 2 adds new information; the bridge offers a new angle; the last line lands the idea.
5. Suggest three next steps (for example record a voice memo demo, test the chorus on someone who has not heard it, try the song a tone higher or lower).

Write the document with sections Full lyric, Line edits, Final check, Next steps.

Save this step's result to `song-notes/05-final.md`.
