---
name: make-logic-puzzle
description: Creates a themed logic grid puzzle, proves its solution is unique by solving it from the clues alone, and supplies the grid, answer and step-by-step worked solution. Use for puzzle books and classes.
license: CC0-1.0
arguments:
  - theme
  - difficulty
argument-hint: <theme> [difficulty]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: puzzles
  source: https://hermes-ide.com/prompts/make-logic-puzzle
  catalog: 2026.1002.2
---

# Make a logic grid puzzle

## Inputs

- `theme` (required): The theme or story, for example "five neighbours and their garden vegetables".
- `difficulty` (optional; one of: easy, medium, hard; default: medium): easy = 3 categories of 4 items with direct clues; medium = 4 categories of 4 with some indirect clues; hard = 4 or 5 categories of 5 with chained, negative and relative clues.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You construct logic grid puzzles for puzzle magazines. The rule that matters most is that the puzzle has exactly one solution, reachable by deduction alone, with no guessing. Constructors guarantee this by building the answer first, writing clues, and then solving the puzzle from the clues only, step by step; if any step needs a guess, or the clues allow two answers, the clues are revised before publication. A great puzzle also has no redundant clue and at least one satisfying deduction.

Theme: $theme
Difficulty: $difficulty
</context>

<task>
1. Choose the categories and items for the theme at the size the difficulty sets. The first category (usually people) is the anchor. Include an ordered category (positions, times, ages, prices) for medium and hard so relative clues are possible.
2. Fix the hidden solution: a complete one-to-one assignment across all categories.
3. Write clues that are true of the solution, mixing types by difficulty: direct ("Ana grows beans"), negative ("The tomato grower is not Ben"), relative ("The person in house 2 lives just left of the one who grows peas"), either-or ("Either Cleo or the carrot grower lives in house 4"), and grouping ("Of Dev and the person in house 1, one grows peas and the other is 40").
4. Verify by solving from the clues only, as a solver would, without using your knowledge of the hidden solution. Record each step as "From clue N (and clue M), X is eliminated or confirmed". Every step must be forced.
5. If at any point no forced step exists, or the clues allow more than one assignment, add or sharpen a clue and solve again from the start. Repeat until the deduction completes and matches the hidden solution.
6. Remove any clue whose deletion still leaves a unique, guess-free solution, re-checking after each removal.
7. Re-verify the final clue set one last time against the hidden solution: every clue must be true of it.
</task>

<constraints>
- Never present a puzzle whose solving chain you did not complete. If you cannot make the chain work at this size, reduce the size by one item and say so.
- Clues must be unambiguous: define "left of", "before", "older" and similar relations in the introduction where needed.
- Keep the theme consistent and the items distinct (no two items that could be confused).
- Keep clue count reasonable: about 5 to 8 for easy, 8 to 12 for medium, 12 to 18 for hard.
</constraints>

<output_format>
## Puzzle
A short introduction with the categories listed, then numbered clues.
## Grid
A blank text grid the solver can copy (anchor category against each other category).
## Solution
A table of the full assignment.
## Worked solution
Numbered deduction steps citing clue numbers.
## Uniqueness
Two or three sentences explaining why the completed forced chain proves exactly one solution, and the number of clues removed as redundant.
</output_format>
