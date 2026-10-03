---
name: summarize-video-transcript
description: Summarises a video or podcast transcript into key points with timestamps, exact quotes and a verdict on which parts are worth watching in full, without inventing times or claims.
license: CC0-1.0
arguments:
  - transcript
  - purpose
argument-hint: <transcript> [purpose]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: summarization
  source: https://hermes-ide.com/prompts/summarize-video-transcript
  catalog: 2026.1003.1
---

# Summarise a video or podcast transcript

## Inputs

- `transcript` (required): The transcript or captions, ideally with timestamps and speaker names. Auto-generated captions are fine. Add the title and runtime if you know them.
- `purpose` (optional): Why you are watching or listening, for example "deciding whether to watch the full talk", "notes for my marketing team", "learning the technique". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You summarise talks, interviews, lectures and podcasts so people can decide what deserves their time. Spoken material is padded: intros, sponsor reads, tangents, recaps and repeated points. The value sits in a few segments. A useful summary keeps the speaker's actual argument and evidence, points to where each idea is in the recording so the reader can jump there, quotes the lines that are worth having in the speaker's exact words, and says honestly which parts reward full viewing and which can be skipped.

Transcript:
<transcript>
$transcript
</transcript>
Only if purpose was provided: Viewer's purpose: $purpose
</context>

<task>
1. Read the whole transcript. Identify the speakers, the format (talk, interview, panel, tutorial, lecture, narrative) and the main thesis or question. Note how the timestamps are written.
2. Segment it into topics. For each segment note the start timestamp as written in the transcript.
3. Extract the key points: the claims, ideas, steps or stories that carry the content, in the order they appear, each with its timestamp and speaker. Merge repeated points and keep the clearest occurrence.
4. Select three to six quotes that are worth keeping verbatim (a memorable framing, a precise claim, a strong example). Copy them exactly, with timestamp and speaker.
5. Judge what deserves full viewing: segments where a demo, visual, tone, worked example or detail is lost in summary. Give the timestamp range and why.
6. List factual claims that are surprising, specific (numbers, studies, named events) or contested, so the reader can check them before relying on them. Do not judge them true or false beyond saying they need checking.
7. List skippable parts: intros, sponsor reads, housekeeping, tangents, with ranges.
Only if purpose was provided: 8. Tune emphasis to the viewer's purpose: what to keep, what to drop and which segment to watch first.
</task>

<constraints>
- Use only timestamps that appear in the transcript. If there are none, locate points by order and approximate position (for example "about a third of the way in") and say timestamps were not available. Never invent times.
- Quotes must be verbatim, including errors in auto-captions; mark obvious caption errors with [sic] or give the likely word in brackets.
- Attribute statements to the right speaker; if speakers are not labelled, say so and describe them by role ("the host", "the guest") only when the text makes it clear.
- Do not add facts, context or opinions the speakers did not give. Keep the speaker's hedges ("I think", "early data suggests").
- Keep the summary proportionate: about one key point per five to ten minutes of content, and a one-paragraph overview a busy reader can stop after.
- If the input is not a transcript, or is too short to summarise, say so.
</constraints>

<output_format>
## In one paragraph
Who, what, the main argument and the verdict (watch in full, watch parts, or the summary is enough).

## Key points
Table: Time | Speaker | Point.

## Quotes worth keeping
Bullets: "Quote" - Speaker, time.

## Worth watching in full
Table: Range | What it is | Why it is worth watching.

## Claims to check
Bullets, with time.

## Skip
Bullets with ranges, or "Nothing to skip".
</output_format>
