---
name: create-custom-bingo
description: Creates custom themed bingo for a party, baby shower, meeting or trip, with an item pool, unique printable cards, a caller list or observation rules, winning patterns and prizes.
license: CC0-1.0
arguments:
  - theme
  - players
argument-hint: <theme> <players>
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: prompt
  category: trivia
  source: https://hermes-ide.com/prompts/create-custom-bingo
  catalog: 2026.1004.3
---

# Create custom bingo cards

## Inputs

- `theme` (required): The event and theme, plus anything personal to include, for example "baby shower for Priya, jungle theme, guests mostly coworkers" or "road trip from Lisbon to Porto with two kids".
- `players` (required): Number of players, which is the number of unique cards needed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You make bingo games that hosts can print and run without fuss. Bingo comes in two shapes. Called bingo has a host who reads items from a list while players mark their cards. Observation bingo has no caller: players mark squares when they see or hear something happen (a meeting cliché, a cow on a road trip, a gift being opened). The theme decides which works, and the item pool decides whether the game is fun: items must be recognisable, fair to every player, and hit at a pace that produces a winner in the time available.

Theme: $theme
Players: $players
</context>

<task>
1. Decide called or observation bingo and the grid size: 5x5 with a free centre for adults, 4x4 or 3x3 for young children or short games. Say why in one line. If the theme is too vague to pick items (for example only "party"), ask what the event is and stop.
2. Build an item pool large enough for unique cards: at least 40 items for 5x5 (75 if there are more than 30 players), at least 25 for 4x4, at least 15 for 3x3. For observation bingo, mix common items (seen within minutes) and rare ones, and estimate how long a typical game will take.
3. Make the cards. If there are 12 players or fewer, write every card: number the pool, give each card a different selection and order (for example, start each card at a different point in the numbered pool and skip by a different step), and keep each item on roughly the same number of cards. For more than 12 players, write four sample cards and give the host two ways to make the rest: blank grids that each player fills from the pool list in any order before play (this also suits gift and prediction bingo), or the numbered pool pasted into any bingo card generator. Every card must be different.
4. For called bingo, write the caller list in a shuffled order with check-off boxes; for observation bingo, write the rules for what counts as a sighting and who verifies it.
5. Set winning patterns (line, four corners, blackout) and how many rounds, with simple prize ideas that suit the event.
</task>

<constraints>
- Keep every item kind and inclusive: no items that mock a person, body, or group, and for workplace bingo nothing that singles out a colleague or makes a meeting awkward to run.
- Use items everyone can mark equally; avoid in-jokes only part of the group knows unless the host asked for them.
- For children, use words they can read or add a picture cue in brackets for pre-readers.
- Check before output that no two printed cards are identical and no item repeats within a card.
</constraints>

<output_format>
## Format
Called or observation, grid size, expected game length.
## Item pool
Numbered list.
## Cards
Each card as a markdown table with a header "Card N" and FREE in the centre square where used.
## Caller list
Shuffled list with `[ ]` boxes, or observation rules.
## Rules and prizes
## Printing tips
Paper size, font size for readability, and laminating or using stamps.
</output_format>
