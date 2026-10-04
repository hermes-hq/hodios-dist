---
name: write-session-recap
description: Turns a game master's rough notes into a read-aloud recap and catch-up bullets safe to share with players, plus a separate GM-only part with loose threads and hooks for the next session.
license: CC0-1.0
arguments:
  - session_notes
  - tone
argument-hint: <session_notes> [tone]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tabletop-rpg
  source: https://hermes-ide.com/prompts/write-session-recap
  catalog: 2026.1004.1
---

# Write a session recap

## Inputs

- `session_notes` (required): Your notes from the last session in any form (bullets, shorthand, a transcript), plus the campaign name, the player characters' names and anything the players must not learn yet.
- `tone` (optional; default: an epic bard's tale with a touch of humour): The voice of the recap, for example "a bard's tale", "a newspaper report", "a grim chronicle", "a sarcastic narrator", "a detective's case notes".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help game masters open each session strong. A recap read at the table reminds players what happened, makes their characters' choices feel important and builds anticipation; a plain summary catches up the player who missed the session. The best recaps are told in a voice that fits the campaign, give every player character a moment, remember the funny moments players still talk about, and end on the open question that drives the next session.

The game master will copy the player-facing part straight into the group chat or read it aloud, so that part must be safe to share as written. Everything the game master knows and the characters do not (a traitor, a hidden motive, what is behind the door) lives only in the GM-only part, and even there it is pointed to, not repeated.

Session notes: $session_notes
Tone: $tone
</context>

<task>
1. Sort the notes before writing. Separate what the characters witnessed or learned at the table from what only the game master knows: lines marked secret, GM-only or "they don't know", plus anything the notes describe that no character was present for. Only the first group may appear in the player-facing part. Note names spelled more than one way and facts that are unclear.
2. Find the story of the session: the key events in order, the decisions the players made, the memorable moments (a critical hit, a terrible plan that worked, a joke), what was gained or lost, and exactly where the session stopped.
3. Write the in-world recap in the requested tone, to be read aloud in one to two minutes (150 to 300 words). Give every player character named in the notes at least one moment, centre the players' choices rather than the game master's plot, and end on the cliffhanger or the decision ahead, at the point where the session stopped.
4. Write the quick version: five to eight plain, out-of-character bullets for a player who missed the session, covering loot, injuries and conditions, promises made, named NPCs met and where the party stands now.
5. Write the GM-only part:
   - Loose threads: unanswered questions, unfulfilled promises, NPCs who will remember the party, and consequences the party set in motion. Here you may use GM knowledge.
   - Hooks for next session: two or three ways to open, each following from a loose thread, with a line the game master could say.
   - Check before sharing: confirm that each GM-only item from step 1 was kept out of the player-facing part, referring to it by where it sits in the notes ("the line marked SECRET at the end of the notes") rather than restating it; list any name you standardised and any fact you were unsure of, so the game master can confirm it before posting.
</task>

<constraints>
- Use only what is in the notes. Do not invent events, outcomes, loot, injuries or dialogue. Short connecting description is fine; anything that changes what happened is not.
- No GM-only information in the player-facing part, not even as a hint, a wink or foreshadowing, unless the notes say to tease it; then tease only what the notes allow.
- Keep names exactly as in the notes. If a name is spelled several ways, use the most frequent one and list the choice under Check before sharing.
- Match the content level of the campaign; keep gore and mature themes at the level the notes suggest.
- If the notes are too sparse for a recap, write a short one from what is there without filling gaps, and ask up to three questions (who fought what, where it happened, where the session ended) in place of the hooks.
</constraints>

<output_format>
Two parts, in this order, separated by a horizontal rule, so the game master can copy the first part as it stands.

**For the players**
## Previously on
The read-aloud recap, then on its own line: (N words, about N minutes).
## The quick version
Bullets.

---

**GM only: do not share**
## Loose threads
## Hooks for next session
Numbered, each with a line in quotes.
## Check before sharing
A checklist.
</output_format>
