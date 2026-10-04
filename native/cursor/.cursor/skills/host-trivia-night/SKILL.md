---
name: host-trivia-night
description: Writes a trivia night with themed rounds, a difficulty curve, accepted alternative answers, numeric tie-breakers and host notes, flagging facts to verify. Use for pub quizzes and parties.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: trivia
  source: https://hermes-ide.com/prompts/host-trivia-night
  catalog: 2026.1004.1
---

# Host a trivia night

## Inputs

- [THEME] (required): The overall theme, or "general knowledge", plus any round ideas you want included.
- [ROUNDS] (optional; default: 5): Number of rounds.
- [QUESTIONS_PER_ROUND] (optional; default: 10): Questions in each round.
- [AUDIENCE] (optional): Who is playing (age range, country, experts or casual, team or solo), so questions are gettable and fair. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write quizzes for pub trivia nights and parties. A good quiz is not a test of obscure facts: most questions should feel gettable by someone on most teams, a few should spark a debate, and the hardest should still produce an "of course!" when the answer is read. Each question has one unambiguous answer, and the host knows in advance which near-misses to accept.

Theme: [THEME]
Rounds: [ROUNDS] of [QUESTIONS_PER_ROUND] questions
Only if [AUDIENCE] was provided: Audience: [AUDIENCE]
</context>

<task>
1. Plan [ROUNDS] rounds that vary in subject and format (straight questions, connections where the answers share a link, "name the year", true or false with a twist, a final round with double points). Give each round a title.
2. Within each round, order questions from easier to harder: about 30 percent easy, 50 percent medium, 20 percent hard. Across the night, start accessible and build.
3. Write each question so it has exactly one correct answer: specify units, dates and scope; avoid "which of these" without options and avoid trick wording.
4. For each answer, list acceptable alternatives (spellings, partial names, nicknames) and what not to accept.
5. Write three tie-breakers with a stable numeric answer (a height, a year, a distance), where the closest guess wins. Name the kind of source that confirms it (for example "the venue's official site"), never a made-up citation.
6. Write host notes: pronunciations, a one-line fun fact to read after selected answers, and timing (about 60 to 90 seconds per question, plus 5 minutes per round for marking).
7. Use only facts you are confident of. Mark any answer you are less sure of, or that can change over time (records, current office holders, "latest" anything), with [verify] and the date your knowledge reflects.
</task>

<constraints>
- Fit the audience: age-appropriate for children, avoid questions answerable only by locals of one country unless the audience is local.
- Mix subjects and avoid a run of questions that favour one kind of player.
- No questions whose answer is a matter of opinion or ongoing dispute.
- Nothing mean-spirited or based on stereotypes.
- Questions that need pictures or audio are allowed only if the user asks; describe what the host must prepare.
- If the full quiz will not fit in one reply, deliver complete rounds in order, say which rounds remain, and continue when asked; never cut a round short to fit.
</constraints>

<output_format>
## Overview
Table: Round | Title | Format | Difficulty.
## Rounds
For each round: the title, then a numbered table: # | Question | Answer | Also accept | Host note.
## Tie-breakers
Numbered, with answers and the source of the number.
## Host notes
Running order, timing, scoring rules, any [verify] items gathered in one list.
## Answer sheet
Compact list of answers by round, for marking.
</output_format>
