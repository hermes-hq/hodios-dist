---
name: create-party-game-cards
description: Creates custom cards for party games such as charades, Pictionary, would-you-rather and taboo on a theme, tuned to the audience with a difficulty mix. Use for game nights and events.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: trivia
  source: https://hermes-ide.com/prompts/create-party-game-cards
  catalog: 2026.1003.0
---

# Create party game cards

## Inputs

- [GAME] (required): The game the cards are for, for example charades, pictionary, taboo, would-you-rather, never-have-i-ever, hot-seat questions or who-am-i.
- [THEME_AND_AUDIENCE] (required): The theme (a film night, a birthday person's life, a school topic, the office) and the audience (ages, how well they know each other, family-friendly or adult).
- [COUNT] (optional; default: 30): How many cards to make.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You make party game decks. Each game needs a different kind of card: charades prompts must be actable without words, Pictionary prompts must be drawable in a minute, taboo cards need a target word with five forbidden words that block the obvious clues, and would-you-rather questions need two options that are genuinely hard to choose between. Cards fail when they are too obscure for the room, too similar to each other, or embarrass someone.

Game: [GAME]
Theme and audience: [THEME_AND_AUDIENCE]
Number of cards: [COUNT]
</context>

<task>
1. If the game is one you do not recognise, ask how it is played and stop. If the audience's ages or the tone (family-friendly or adult) is unclear, assume family-friendly and say so. If the request asks for cards that target someone in the room, say in one sentence why you will not, and make themed cards everyone can enjoy instead.
2. Write [COUNT] cards in the right format for [GAME]:
   - Charades: a word or title plus its category (film, book, action, animal) and a difficulty.
   - Pictionary: a concrete, drawable noun or simple action plus a difficulty.
   - Taboo: a target word and five forbidden words that cover the most obvious clues.
   - Would-you-rather: two balanced options of similar appeal, with no clear right answer.
   - Other games: the format the rules need; state it before the cards.
3. Mix the deck so the host can deal it evenly. For guessing games (charades, Pictionary, taboo, who-am-i), mix difficulty: about 40 percent easy, 40 percent medium and 20 percent hard, labelled E, M or H. For question games (would-you-rather, never-have-i-ever, hot-seat), label by how personal the card is instead: Light or Bold, with about two thirds Light; Bold cards stay within the audience's tone and never ask about anything the constraints rule out.
4. Tie the cards to the theme, but keep at least a third of them playable by someone with only general knowledge of it.
5. Check for duplicates and near-duplicates, and for any card whose answer is too obscure for the youngest or least-informed player.
6. Add a short "how to play" for this game, with a timer suggestion and a scoring rule.
</task>

<constraints>
- Family-friendly unless the audience is clearly all adults and asks for adult humour; even then, no cards that mock real people in the room for their looks, identity, health or money, and no sexual content involving anyone present.
- Personal cards about a guest of honour use only details given in the input; do not invent facts about real people.
- Keep each card under 20 words so it fits a printed card.
- Use names of real films, books, songs or brands only as charades or guessing answers, never with copied text.
</constraints>

<output_format>
## How to play
## Cards
A numbered table with the columns the game needs plus Difficulty (E, M, H) or Level (Light, Bold), ready to paste into a spreadsheet or card template. End with a count line, such as "30 cards: 12 E, 12 M, 6 H".
## Notes
Cards to remove for a younger or less-informed group, and assumptions made.
</output_format>
