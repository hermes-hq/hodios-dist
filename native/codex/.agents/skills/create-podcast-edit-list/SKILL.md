---
name: create-podcast-edit-list
description: Creates an edit list from an episode transcript with cuts, tightening, moves, pickups and the best running order, without changing anyone's meaning. Use before editing an episode.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: podcasting
  source: https://hermes-ide.com/prompts/create-podcast-edit-list
  catalog: 2026.1004.0
---

# Create a podcast edit list

## Inputs

- [TRANSCRIPT] (required): The raw episode transcript, ideally with timestamps and speaker labels. Add a line on the episode's purpose if it is not obvious.
- [TARGET_MINUTES] (optional): Target length of the finished episode in minutes. Leave empty to cut to what the content supports.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a podcast story editor working from a transcript before anyone touches the audio. The editor's job is to keep the listener: cut what the listener would skip, tighten what drags, and reorder so the episode builds, while keeping every speaker's meaning intact. Typical cuts are housekeeping ("can you hear me?"), false starts, repeated answers, long tangents, inside jokes with no payoff, crosstalk, and the slow warm-up most interviews have in the first minutes. Tightening means removing filler and restarts inside an answer that stays. Moves bring the strongest material earlier or group related topics. Ethical editing never joins words from different answers to make someone say something they did not say, and never removes context that changes the meaning of what remains.
</context>

<task>
<transcript>
[TRANSCRIPT]
</transcript>

Only if [TARGET_MINUTES] was provided: Target length: [TARGET_MINUTES] minutes.
If no target length is given above, cut to what the content supports and say what length that is.

1. **Find the spine.** In two or three sentences: what the episode is about, the single best moment, and what the listener should leave with. Everything is judged against this.
2. **Map the raw episode** into numbered segments with start time (or first words if there are no timestamps), speaker, topic and a keep, tighten, cut or move verdict.
3. **Propose the running order**: the segments in their new sequence, with a one-line reason for each move, aiming for a strong first two minutes, a build to the best moment, and a clean ending.
4. **Write the edit list.** For each action: the location (timestamp range or quoted first and last words), the action (cut, tighten, move, keep), what exactly to remove, and why. Group tightening notes so the audio editor can work in one pass.
5. **Pickups.** Lines the host should record to bridge cuts or moves (a new segue, a context line, a corrected fact), written in the host's voice.
6. **Cold open candidates.** Two or three self-contained moments of 10 to 30 seconds that would hook a listener, with their locations.
7. **Estimate the time** before and after, using timestamps if present, otherwise about 150 words per minute.
</task>

<constraints>
- Never suggest joining words or phrases from different answers into a new sentence, and never cut a qualifier ("I think", "in our case", "not") when removing it changes the claim. If a cut risks changing meaning, flag it.
- Flag anything that may need legal or ethical review before release: claims about named people or companies, private information about third parties, medical or financial advice, or a guest asking for something to be off the record.
- If the transcript has no timestamps, reference locations by quoted first and last words and say the time estimate is approximate.
- If the target length would force cutting the best moment or essential context, say so and propose the shortest honest length.
- Keep it to an edit plan; do not rewrite guest answers.
</constraints>

<output_format>
## Episode spine
## Running order
A numbered list of segments in the new order with reasons for moves.

## Edit list
A table: # | location | action | what to remove or move | why.

## Pickups
Each pickup line with where it goes.

## Cold open candidates
## Time estimate
Raw length, cut length and the main savings. Then any flags for review.
</output_format>
