---
name: create-escape-room-puzzles
description: Designs a themed chain of escape-room puzzles with a flow map, solutions, props, reset steps and three-step hint ladders, timed to the session. Use for home games, parties and classrooms.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: puzzles
  source: https://hermes-ide.com/prompts/create-escape-room-puzzles
  catalog: 2026.1003.1
---

# Create escape-room puzzles

## Inputs

- [THEME] (required): Theme and story, plus where it will run (living room, classroom, venue) and any budget or props you already have.
- [PLAYERS] (optional; default: 4): Number of players.
- [DURATION_MINUTES] (optional; default: 60): Time limit in minutes.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design escape rooms, from commercial venues to birthday parties. A good room is a chain of "aha" moments that a group solves together: every puzzle is fair (the clues are in the room), each solution unlocks something that leads onward, nobody stands idle, and the game master can rescue a stuck team with a hint without giving the game away.

Theme: [THEME]
Players: [PLAYERS]
Time limit: [DURATION_MINUTES] minutes
</context>

<task>
1. Write the story and goal in three sentences: who the players are, what they must do, and why the clock is running.
2. Design the flow: a mostly parallel structure with two or three tracks that merge into a final meta-puzzle, so a group of [PLAYERS] can split up. Aim for one puzzle per one or two players at any time. Show it as a text flow map.
3. Design five to nine puzzles, varied in type (search, cipher, pattern, logic, physical, observation, teamwork). For each: what the players find, what they must figure out, the solution, what it unlocks, the props, and the estimated solve time.
4. Write a three-step hint ladder for each puzzle: a nudge (where to look), a direction (what to try), and the answer.
5. Design a finale that uses something from each track.
6. Check timing: the sum along the longest path should be about 70 to 80 percent of [DURATION_MINUTES] minutes, leaving room for wandering. Adjust the number of puzzles to fit.
7. List props with low-cost alternatives (printables, combination padlocks, envelopes, UV pens) and a reset checklist.
</task>

<constraints>
- Every puzzle is solvable from what is in the room; no outside knowledge beyond what the stated audience can be expected to have.
- No red herrings unless the user asks; if any, mark them clearly for the game master.
- Every lock or code has exactly one valid answer, and the answer format (four digits, a word, a colour order) is signposted on the lock or the puzzle.
- Safety: never lock real exits or lock anyone in; nothing that needs climbing, heavy lifting, flames or small parts for young children.
- Fit the setting: a home game uses household space and a printer; a venue may use built props.
</constraints>

<output_format>
## Story and goal
## Flow map
A text diagram of tracks and dependencies.
## Puzzles
One subsection per puzzle: Find, Figure out, Solution, Unlocks, Props, Time, Hints (1, 2, 3).
## Finale
## Props list
Table: Item | Used in | Cheap alternative.
## Reset checklist
## Running the game
Briefing script (under 100 words), when to offer hints, and the debrief.
</output_format>
