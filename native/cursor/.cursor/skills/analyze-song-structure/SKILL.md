---
name: analyze-song-structure
description: Analyses a song's sections, hook placement, chord movement, rhyme scheme, prosody and dynamics to show why it works, with lessons and exercises for your own writing. Use to study songs.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: music
  source: https://hermes-ide.com/prompts/analyze-song-structure
  catalog: 2026.1003.0
---

# Analyse a song's structure

## Inputs

- [SONG_LYRICS_OR_DESCRIPTION] (required): The song's lyrics with section labels if you know them, or a description of how it goes (sections, chords, tempo, where it builds). Add the title and artist, the chords if you know them, and what you want to learn from it.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Songwriters learn most by taking apart songs that work. A useful analysis goes beyond labelling sections: it shows how quickly the song reaches its hook, how each section differs from the next in melody range, rhythm, line length and harmony, how the title is set up and paid off, how the verses move the story, and how the arrangement builds and releases energy. Analyses go wrong when they invent chords or facts about a recording the analyst cannot verify, quote full copyrighted lyrics from memory (often wrongly), or describe without drawing transferable lessons.
</context>

<task>
Analyse this song:

<song>
[SONG_LYRICS_OR_DESCRIPTION]
</song>

1. **Snapshot:** title and artist if given, genre, the song's central idea in one sentence, and what the user wants to learn (if stated). Work from the material provided. If only a title is given, analyse from what you reliably know of its structure and sound, say clearly what you are unsure of, do not reproduce its lyrics from memory, and invite the user to paste the lyrics or chords for line-level analysis.
2. **Song map:** a table of sections in order (intro, verse, pre-chorus, chorus, post-chorus, bridge, breakdown, outro) with approximate length in lines or bars, the job each section does (sets the scene, builds tension, delivers the hook, gives a new angle) and its energy level from 1 to 5. Note how long it takes to reach the first chorus and the title.
3. **Hook:** where the title and any secondary hooks sit (first or last line of the chorus, repeated tags, an instrumental riff, a post-chorus chant), how often the title recurs, and how the verses or pre-chorus set it up so it lands.
4. **Harmony:** if chords were provided or the user stated them, give them per section with Roman numerals relative to the key, and explain the movement (loops, borrowed chords, where the chorus starts on the tonic or avoids it, how the bridge shifts colour). If no chords are given and you are not certain of them, describe the likely harmonic function in general terms and say it is unverified; never present guessed chords as fact.
5. **Lyrics and rhyme:** rhyme scheme per section with letters, rhyme types (perfect, slant, internal, multisyllabic), point of view and any shift, how verse 2 develops verse 1, concrete images versus statements, and prosody (whether stressed syllables fall on strong beats; short choppy lines versus long flowing ones and what that does to the feeling). Quote only short fragments from the provided text, enough to make a point.
6. **Dynamics and arrangement:** how the song builds and releases energy (instrument entries and drop-outs, rhythm changes, vocal range rising into the chorus, a stripped-down final chorus, a key change), from what was described or what you reliably know.
7. **Why it works:** three to five principles, each tied to specific evidence above.
8. **Lessons for your writing:** three exercises that apply those principles to the user's own songs (for example "write a pre-chorus that shortens the line length by half", "put your title as the last line of the chorus and build the verse to point to it").
</task>

<constraints>
- Do not reproduce full copyrighted lyrics, even if you believe you remember them. Use short fragments from the text the user provided.
- Do not invent facts about the recording, the writers, chart positions or the song's backstory. Say "I don't know" where you are unsure.
- Mark interpretation as interpretation.
</constraints>

<output_format>
Use the sections in order as level-two headings. The Song map is a table: Section | Length | Job | Energy (1 to 5).
</output_format>
