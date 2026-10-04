---
name: critique-speech-recording
description: Reviews a transcript of a rehearsed or delivered talk for pacing, filler words, structure, clarity and audience connection, with timestamped notes and three targeted drills.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: public-speaking
  source: https://hermes-ide.com/prompts/critique-speech-recording
  catalog: 2026.1004.3
---

# Critique a speech recording

## Inputs

- [TRANSCRIPT] (required): The transcript of your talk, ideally with timestamps and with filler words kept (turn off any "clean up" option in the transcription tool).
- [TALK_GOAL] (optional): Optional: what the talk was meant to achieve and for whom, for example "get the board to approve the hire" or "best-man toast, 80 guests".
- [DURATION_MINUTES] (optional): Optional: how long the talk took, in minutes, if the transcript has no timestamps. Used to work out speaking pace.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A transcript is an honest mirror of a talk: it shows the filler words, false starts, rambling middles, missing signposts and weak endings that speakers do not notice while speaking. Useful feedback is specific and located (this sentence, at this point), separates habits worth fixing from normal speech, and turns into a few drills the speaker can practise, rather than a long list of everything imperfect. Conversational speech runs at roughly 120 to 160 words a minute; a few fillers are normal and invisible to audiences, while clusters of them, or a habit like ending every sentence with "right?", are noticed.
</context>

<task>
Review this talk.

<transcript>
[TRANSCRIPT]
</transcript>
Only if [TALK_GOAL] was provided: Goal: [TALK_GOAL]
Only if [DURATION_MINUTES] was provided: Duration: [DURATION_MINUTES] minutes.

1. If the text is not a spoken transcript (for example it is a written script with no sign of delivery), say that this review works best on a transcript of the talk as delivered, review the structure and clarity only, and skip the delivery numbers.
2. Measure: total words; pace in words per minute if timestamps or a duration are available (otherwise say it cannot be measured; with timestamps only, note that the last timestamp marks the start of the final line, so the true duration is slightly longer); counts of each filler ("um", "uh", "like", "you know", "so", "basically", "right?", "kind of") and fillers per minute; repeated phrases or verbal tics; the longest sentence.
3. Assess, quoting the transcript:
   - Opening: does it earn attention and state why this matters within the first 30 seconds?
   - Structure: is the main point clear, are there signposts, does the middle wander?
   - Clarity: jargon, long or tangled sentences, vague words where a specific would land.
   - Audience connection: "you" language, examples, questions, stories.
   - Ending: is there a clear close or does it trail off ("so yeah, that's it")?
4. Write located notes: each with a timestamp (or the opening words of the sentence if there are no timestamps), the issue, and a rewrite or fix.
5. Pick three drills targeted at the biggest issues, each with how to practise it in under ten minutes.
</task>

<constraints>
- Lead with what worked, specifically, before what to fix. Name at most eight notes, most important first.
- Count only what is in the transcript, and label counts on long transcripts as approximate. Say that automatic transcripts may drop fillers or mishear words, so counts are a lower bound. Count "so" and "like" only when they are fillers, not when they carry meaning ("so that", "I like").
- Do not judge accent, dialect or grammar that is normal in the speaker's variety of the language, unless it blocks understanding.
- If the talk goal is given, judge everything against it.
- Be direct and kind; no vague praise ("great energy!") and no harshness.
</constraints>

<output_format>
## Summary
Three lines: the strongest thing, the biggest issue, and the one change that would help most.
## By the numbers
A table: Measure | Value | Typical range or note.
## Notes
A table: Where | Issue | Try instead.
## Drills
Three numbered drills with steps and time needed.
## What a transcript can't show
One or two lines: tone, pauses, eye contact and body language, and a suggestion to record video for the next round.
</output_format>
