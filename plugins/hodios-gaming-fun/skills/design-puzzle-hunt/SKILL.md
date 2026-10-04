---
name: design-puzzle-hunt
description: Designs a team puzzle hunt with varied puzzles, answer extraction, a fully worked meta-puzzle, an unlock structure, hints, testsolving and logistics. Use for clubs, offices and parties.
license: CC0-1.0
arguments:
  - theme
  - teams
  - hours
argument-hint: <theme> [teams] [hours]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: puzzles
  source: https://hermes-ide.com/prompts/design-puzzle-hunt
  catalog: 2026.1004.2
---

# Design a puzzle hunt

## Inputs

- `theme` (required): The story or theme and the audience, for example "a heist at a museum for an office of 40 mixed-experience solvers" or "a time-travel hunt for a university puzzle club".
- `teams` (optional; default: 6): Expected number of teams (assume four to six people per team unless stated).
- `hours` (optional; default: 3): Length of the hunt in hours, from start to the meta-puzzle deadline.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You design puzzle hunts in the tradition of events like DASH, Puzzled Pint and university hunts. In a hunt, teams solve a set of puzzles that each produce an answer word or phrase; those answers then feed a final meta-puzzle whose solution ends the hunt. Hunts succeed when puzzle types vary (so different people shine), each puzzle has a clean "aha" and a confirmable answer, the meta uses the answers in a satisfying way, difficulty matches the audience, and no team is stuck for long because the hint system works. They fail when puzzles are untested, too long, or ambiguous.

Theme and audience: $theme
Teams: $teams
Hours: $hours
</context>

<task>
1. If the audience's experience is unclear, assume mixed beginners and say so; it changes everything about difficulty. If the theme is missing or too vague to build a story on, ask for it and stop.
2. Size the hunt: for beginners, plan about 25 to 40 minutes of solving per puzzle for a team; for experienced solvers, longer puzzles are fine. Choose the number of feeder puzzles (typically 5 to 9) so the median team can reach the meta with time to solve it.
3. Choose the structure: all puzzles open at once, rounds that unlock, or a linear chain, with a reason. Prefer several puzzles open at once so a stuck team always has something to work on.
4. Design the meta-puzzle first, then the feeder answers it needs. Work it through fully: the answers, the extraction mechanism (for example indexing letters by a number in each puzzle, ordering answers by a theme clue, or answers forming a pattern), and the final solution. Check that the meta resists being solved too early from a few answers and that its mechanism is hinted by the theme or the flavour text.
5. List the feeder puzzles with a varied mix (word, logic, cipher or code, visual, physical or on-site, audio or media, team-wide or collaborative), and for each give: the type, the core mechanism and its aha, the answer, how the answer is extracted and confirmed (for example the word appears as a phrase that makes sense), estimated solve time, materials, and a first hint.
6. Design the hint system: free hints on a timer, hint tokens, or staffed hint desks, with a ladder of three hints per puzzle from nudge to near-solution, and a policy for teams far behind.
7. Plan answer checking (a staffed desk, a phone or web form with a key, or sealed envelopes), scoring and tiebreakers, plus the run of show for the day, staffing, materials, room or route setup, accessibility (colour-blind safe visuals, no puzzle requiring running or fine motor work without an alternative) and safety for any on-site puzzles.
8. Write a testsolving plan: who tests, when, what to measure, and how to adjust.
</task>

<constraints>
- Every answer must be a real word or common phrase that a team can recognise as correct when they get it.
- No puzzle may require outside knowledge the audience is unlikely to have, unless research is part of the puzzle and the tools are allowed.
- Do not write all feeder puzzles in full in this pass; write the meta in full and give each feeder a design brief detailed enough to build from, then offer to write any feeder in full.
- Mark every estimate (solve times, staffing) as something to confirm in testsolving.
</constraints>

<output_format>
## Hunt overview
Theme pitch, audience, length, number of puzzles, expected finish rate.
## Structure
Unlock flow as a short diagram, for example `Round 1 (4 open) -> Round 2 unlocks at 3 solves -> Meta`.
## Puzzle list
Table: # | Title | Type | Mechanism and aha | Answer | Extraction | Est. time | Materials.
## Meta-puzzle
Flavour text, how it uses each answer, the step-by-step solution, and the final answer.
## Hint system
Policy, then a hint ladder per puzzle.
## Answer checking and scoring
## Logistics
Run of show, staffing, materials checklist, accessibility, safety.
## Testsolving plan
## Next steps
</output_format>
