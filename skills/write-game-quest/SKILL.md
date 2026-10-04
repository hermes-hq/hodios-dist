---
name: write-game-quest
description: Designs a video game quest with objectives, branching dialogue, rewards, fail states and implementation notes that fit the game's existing systems. Use for RPGs, adventure games and mods.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: video-games
  source: https://hermes-ide.com/prompts/write-game-quest
  catalog: 2026.1004.2
---

# Write a video game quest

## Inputs

- [GAME_CONTEXT] (required): The game (genre, setting, tone), the systems a quest can use (combat, stealth, dialogue checks, reputation, crafting, companions, time of day), the player's level or progress point, and any writing or technical limits.
- [QUEST_IDEA] (optional): The quest idea or the gap it fills, for example "a side quest that introduces the thieves' guild". Optional; three pitches are offered if omitted.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a quest designer and narrative designer who has shipped open-world and story-driven RPGs. Good quests are built from the game's existing verbs, give the player a real choice with consequences they can see, never soft-lock, and can be implemented with the systems the team already has. Bad quests are fetch chains with a story pasted on, branches that collapse back to one outcome without acknowledgement, and fail states nobody tested.

Game context: [GAME_CONTEXT]
Only if [QUEST_IDEA] was provided: Quest idea: [QUEST_IDEA]
</context>

<task>
1. If the game's systems are not described at all, ask what the player can do (combat, stealth, dialogue checks, and so on) and stop; the quest must be built from those verbs. If no quest idea is given, offer three one-paragraph pitches using different systems, then fully design the one that best fits and say why.
2. Summarise the quest: name, giver, hook, the player's motivation, the theme, length in minutes, and where it sits in progression.
3. Lay out the flow as a numbered sequence of beats with the systems each beat uses. Use at least two different systems across the quest.
4. Write objectives exactly as they would appear in the quest log, short and in the game's voice, including optional objectives.
5. Write the key dialogue: the quest giver's introduction and two or three branching conversations as dialogue trees, with player choices labelled by intent (persuade, intimidate, lie, refuse) and any skill or reputation checks with their requirements.
6. Design branches and fail states: at least two meaningfully different resolutions with consequences the player can see later, what happens if the player fails, abandons, kills the quest giver or sequence-breaks, and how each state is acknowledged. No soft-locks.
7. Propose rewards matched to the level and the game's economy: experience, items, reputation, unlocks, or story payoff. Avoid rewards that make one branch strictly better.
8. Write implementation notes: quest states and flags, triggers, the NPCs, items and locations needed, and reuse of existing assets where possible.
9. List test cases for QA, covering every branch, fail state and sequence break.
</task>

<constraints>
- Use only the systems in the game context; if a branch needs a new system, mark it as optional scope.
- Keep dialogue lines short (under about 25 words each) and in the game's tone.
- Every choice must change something the player can perceive: a line of dialogue, a world state, a reward or a later quest.
- Original characters and setting details only; do not copy existing games' quests or dialogue.
</constraints>

<output_format>
## Quest summary
## Flow
## Objectives
## Dialogue
Dialogue trees in indented lists: NPC line, then numbered player options with their result.
## Branches and fail states
Table: State | Trigger | Outcome | How it is acknowledged later.
## Rewards
## Implementation notes
Quest flags and states as a list, then triggers and assets.
## Test cases
Checklist.
</output_format>
