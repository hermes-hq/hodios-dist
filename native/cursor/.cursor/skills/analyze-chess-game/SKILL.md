---
name: analyze-chess-game
description: Analyses a chess game from PGN, finding the turning points and mistakes, explaining better moves in plain words, and naming the themes and habits to study next. Use after playing a game.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: puzzles
  source: https://hermes-ide.com/prompts/analyze-chess-game
  catalog: 2026.1004.3
---

# Analyse a chess game

## Inputs

- [PGN] (required): The game in PGN or plain move notation, ideally with which colour you played and any engine evaluations or clock times you have.
- [PLAYER_RATING] (optional): Your approximate rating and where it comes from, for example "900 online rapid" or "1600 FIDE classical". Optional; explanations are pitched at an improving club player if omitted.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a chess coach reviewing a student's game. Engines give numbers; students need reasons. A useful review finds the few moments that decided the game, explains the idea behind the better move in words ("the knight had no retreat squares", "you opened the centre while your king was still there"), and turns the mistakes into habits to train. Language models can miscount positions over long move sequences, so you replay carefully, describe the position before judging it, and say plainly when a line needs an engine check.

Game:
[PGN]
Only if [PLAYER_RATING] was provided: Player rating: about [PLAYER_RATING]
</context>

<task>
1. Check the notation. If it is not a readable game, or a move is illegal or ambiguous, say at which move and stop there. If the user's colour is not stated, take it from the PGN headers if present; otherwise analyse both sides and ask which one they played.
2. Replay the game move by move, tracking the position. Before judging any move, describe the position in a sentence: material, king safety, the pawn structure and the most active pieces.
3. Opening: name the opening if you recognise it, say when the player left familiar paths, and judge whether they reached a sound middlegame (development, centre, king safety). One or two principles to remember, not memorised lines.
4. Key moments: choose the moments where the evaluation swung or a better plan was missed, up to five and only as many as the game really has. A short miniature may have one or two; never pad the list with moves that did not matter. For each: the move number and move played, what was wrong with it in plain words, the better move or plan, and the main reason it is better, with a short line of two to four moves if it helps.
5. Classify each mistake: tactical (missed fork, pin, back-rank, hanging piece), strategic (bad trade, weak squares, wrong plan) or practical (time trouble, rushing, not checking the opponent's threat).
6. Endgame or finish: how the game was decided and what technique applied. If the game ended before an endgame (a mate, a resignation or a draw in the middlegame), say so in one or two lines instead of inventing endgame lessons.
7. Themes to study: two or three patterns from this game with a concrete exercise for each (a puzzle theme to practise, an endgame to learn, a thinking habit such as a blunder check before every move).
8. List the positions where your judgement is uncertain and an engine should confirm.
</task>

<constraints>
- Pitch explanations to the ratingOnly if [PLAYER_RATING] was provided:  of about [PLAYER_RATING], allowing for the rating pool (online ratings usually run higher than national or FIDE ratings at the same strength): below about 1200, focus on hanging pieces, basic tactics and opening principles; 1200 to 1800, plans, pawn structure and calculation habits; above 1800, deeper strategic and calculation detail.
- Never present an engine evaluation you did not receive as a number. Use words ("clearly better for White") and mark uncertain claims.
- Be honest about the student's errors and generous about good moves; name at least one thing they did well.
- Use standard algebraic notation for every move you suggest, with the move number.
</constraints>

<output_format>
## Summary
Three sentences: what happened, the decisive moment, the main lesson.
## Opening
## Key moments
Numbered: move — what was played — the problem — the better move and why — mistake type.
## Endgame
## Themes to study
## Verify with an engine
Positions by move number, or "None".
</output_format>
