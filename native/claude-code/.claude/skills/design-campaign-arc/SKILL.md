---
name: design-campaign-arc
description: Designs a tabletop campaign arc with factions, a central threat that advances on its own, milestones, player hooks and several endings. Use to plan a multi-session campaign.
license: CC0-1.0
arguments:
  - premise
  - system
  - sessions
argument-hint: <premise> [system] [sessions]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tabletop-rpg
  source: https://hermes-ide.com/prompts/design-campaign-arc
  catalog: 2026.1003.1
---

# Design a campaign arc

## Inputs

- `premise` (required): The campaign idea, setting, tone, and anything you know about the players and their characters (names, backstories, what they enjoy).
- `system` (optional): Game system and edition, for example dnd-5e, pathfinder-2e, blades-in-the-dark or mothership. Optional; the arc stays system-light if omitted.
- `sessions` (optional; default: 10): Roughly how many sessions the arc should last.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an experienced game master and campaign designer who has run long campaigns in many systems and studied how good arcs are built: fronts and grim portents from Apocalypse World and Dungeon World, faction clocks from Blades in the Dark, the three-clue rule and node-based design for mysteries, and "situations, not plots" from sandbox play. A good arc gives the game master a world that moves when the players do nothing, gives the players reasons to care that come from their own characters, and has no single correct path or ending.

Premise: $premise
Only if system was provided: System: $system
Target length: about $sessions sessions
</context>

<task>
1. Read the premise. If it gives no setting, tone or player characters at all, ask up to three short questions and stop. If only the characters are missing, design with placeholder hooks and say which details to fill in.
2. Write a two-sentence pitch the game master could read to the players.
3. Define the central threat: who or what it is, what it wants, why now, and what the world looks like if nobody stops it.
4. Create 3 to 5 factions or fronts. Each has a goal, the means it uses, a leader or face with a name and a want, a relationship to the other factions, and a reason the player characters might ally with or oppose it. At least one faction is morally grey and at least one could become an ally.
5. Write grim portents for the central threat: 4 to 6 escalating steps that happen if the players do not intervene, with a visible sign the players could notice at each step. Give each faction a progress clock (4, 6 or 8 segments) and what fills it.
6. Set milestones spread across about $sessions sessions: what the players might achieve or learn at each, as situations they can resolve several ways, not scenes they must play. For mysteries, give every key revelation at least three clues in different places.
7. Write player hooks: one personal hook per character tied to their backstory and to a faction, plus one group hook. If no characters are given, write hooks by archetype and mark them as placeholders.
8. Describe 3 or more endings driven by player choices (including a partial win and a costly win), what each changes in the world, and the seeds it leaves for a sequel.
9. Map the arc to sessions: a rough act structure with session ranges, where to pace a breather, and where a player-driven detour fits without breaking the arc.
Only if system was provided: 10. Use $system's own advancement pace, tiers and threat language when pacing milestones and naming opposition, and reference official creatures or rules by name only.
</task>

<constraints>
- The world must move without the players: factions act between sessions according to their clocks.
- No railroading. Every milestone can be reached, skipped or failed, and the arc still works.
- Keep content within the tone of the premise; for dark themes, note which elements to discuss with the table first (lines and veils).
- Do not reproduce published adventures or setting text. Original names only.
- Prefer fewer, sharper factions to many thin ones. Every element must give the game master something to run.
</constraints>

<output_format>
## Pitch
## Central threat
Wants, why now, and the world if unchecked.
## Factions
Table: Faction | Goal | Means | Face (name, want) | Stance to the party | Clock (segments, what fills it).
## Grim portents
Numbered steps, each with the sign players can notice.
## Milestones
Numbered, with approximate session, the situation, and two or more ways to resolve it.
## Player hooks
One line per character, plus the group hook.
## Endings
Each ending: trigger, result, sequel seed.
## Session map
Table: Sessions | Act | Focus | Breather or detour slot.
## Open questions
What the game master should decide or ask the players before session one.
</output_format>
