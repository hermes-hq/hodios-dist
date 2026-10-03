---
name: session-prep-track
description: Preps a tabletop session in gated steps, from a recap and player hooks through scenes, encounters and NPCs to a one-page cheat sheet. Use before each session of an ongoing campaign.
license: CC0-1.0
arguments:
  - campaign_notes
  - system
argument-hint: <campaign_notes> [system]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: tabletop-rpg
  source: https://hermes-ide.com/prompts/session-prep-track
  catalog: 2026.1003.0
---

# Session prep track

## Inputs

- `campaign_notes` (required): Notes from the last session(s), the campaign's current situation, active threads, the player characters, and anything planned for next time.
- `system` (optional): Game system and edition, for example dnd-5e, pathfinder-2e or blades-in-the-dark. Optional; encounters stay system-light if omitted.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Preps the next session of a running campaign from the game master's notesOnly if system was provided:  for $system, one approved step at a time: a recap and state of play, then hooks for each player character, then scenes and encounters, then the NPCs, then a one-page cheat sheet to run from. Prep is for situations, not scripts: every step prepares material the game master can use in any order, so nothing is wasted if the players go somewhere unexpected. Each step stops for the game master's approval or edits, and later steps build on the approved versions. If the game master asks to skip the approvals, confirm once, then run the remaining steps in one reply and state each choice made at a skipped gate. Never invent past events: anything not in the notes is marked as a suggestion.

## Steps

Work through these steps in order. Do not skip a gate.

1. recap (plan)
2. hooks (plan)
3. scenes (design)
4. npcs (design)
5. cheat-sheet (build)

### Step 1: Recap and state of play

Turn the notes into a clear picture of where the campaign stands.

Campaign notes:
$campaign_notes
Only if system was provided: System: $system

1. If the notes give no picture of the party or of what happened last session, ask for both in one message and stop. If only some details are missing (character names, goals, the party's level), carry on and list them under step 4 so the game master can fill them in.
2. Write a player-facing recap of the last session in 5 to 8 sentences, in the past tense, ready to read aloud or post in the group chat. Include only what the characters know.
3. Write the game master's state of play:
   - **Where the party is** and what they were doing when the session ended (a cliffhanger, a rest, mid-dungeon).
   - **Active threads:** open quests, promises, debts and mysteries, each with its status.
   - **What the world did off-screen:** for each villain or faction in the notes, one thing they did since last session, marked as a suggestion if the notes do not say.
   - **Loose ends** the players seemed to care about, judged from the notes.
4. List anything in the notes that is contradictory, unclear or missing, including details later steps will need (each character's name and goals, the party's size and level).

Stop and wait for the game master to approve or correct the recap and state of play.

**Gate:** stop here and wait for the user's approval before step 2 (hooks).

### Step 2: Player hooks and a strong start

Make the session about these characters.

1. For each player character, write one hook for this session tied to their backstory, goals or a choice they made earlier: a person who shows up, a message, a consequence, or a temptation. Note which active thread it connects to.
2. Write a strong start: an opening scene that begins in action or with an immediate choice, within five minutes of play, and follows from where the last session ended. Offer two options: one high-energy, one quieter.
3. Write 8 to 10 secrets and clues: short facts the players could discover this session, each written so it can be found in any scene (from an NPC, an object, a location). Mark which threads each one advances.
4. Name one thread to give a satisfying payoff this session, so the players feel progress.

Stop and wait for the game master to approve, cut or swap hooks before scenes are built.

**Gate:** stop here and wait for the user's approval before step 3 (scenes).

### Step 3: Scenes, locations and encounters

Prepare situations the players can approach in any order.

1. Build 3 to 6 scenes for a typical session length, each with: its purpose, the location with three evocative details, what is here to interact with, the obstacle or tension, and at least two ways through it (fight, talk, sneak, trick, avoid).
2. Mix the pillars: combat, exploration and social interaction. Include at least one scene where no fight is needed.
3. For each combat, build the encounter with the system's own guidelines for this partyOnly if system was provided:  in $system: show the budget or difficulty arithmetic, use official creatures by name rather than inventing statistics, and give the terrain a feature that changes tactics. Note how to scale it up or down by one step on the fly. If the party's size or level is unknown, ask for it before balancing.
4. Add one complication to use if the session drags, and one scene that can be cut if time is short.
5. Mark where the secrets and clues from step 2 could surface in each scene.

Stop and wait for the game master to approve the scenes.

**Gate:** stop here and wait for the user's approval before step 4 (npcs).

### Step 4: NPCs

Give the game master people they can play at a moment's notice.

1. List every NPC the approved scenes need, plus returning characters from the notes likely to appear.
2. For each, give: name (with pronunciation if unusual), role in this session, what they want right now, what they know (linked to the secrets and clues), a voice or mannerism the game master can perform, and how they react if the party is friendly, hostile or dishonest.
3. Keep returning NPCs consistent with the notes; flag any change in their situation since last time as a suggestion.
4. Add three spare names that fit the setting for improvised characters.

Stop and wait for the game master to approve the NPCs.

**Gate:** stop here and wait for the user's approval before step 5 (cheat-sheet).

### Step 5: One-page cheat sheet

Condense the approved prep into a single page to run the session from.

Use short lines, not paragraphs, in this order:

1. **Recap** to read aloud (from step 1, trimmed to three sentences).
2. **Strong start** (the chosen option).
3. **Player hooks:** one line per character.
4. **Scenes:** a bullet per scene with the location, the obstacle, the ways through, and the creatures with their scaling note.
5. **Secrets and clues:** a checklist to tick off during play.
6. **NPCs:** name, want, voice in one line each.
7. **Treasure and rewards** suggested for this session, matched to the system's guidance and marked as suggestions.
8. **If the session drags / if time is short:** the complication and the scene to cut.
9. **Spare names** and a reminder to note what happened for next session's recap.

End with a three-item "after the session" checklist: update the thread list, note what each player enjoyed, and move unused secrets to next time.
