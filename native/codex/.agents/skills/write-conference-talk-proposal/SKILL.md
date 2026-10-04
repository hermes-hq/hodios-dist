---
name: write-conference-talk-proposal
description: Writes a CFP submission with title options, abstract, timed outline, takeaways and notes for reviewers, aimed at the event's audience and selection criteria. Use for engineers and developer advocates.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/write-conference-talk-proposal
  catalog: 2026.1004.2
---

# Write a conference talk proposal

## Inputs

- [TALK_IDEA] (required): What the talk is about, the story or project behind it, what you learned, any results or numbers, and what you want attendees to do differently afterwards.
- [CONFERENCE] (optional): The event and track, its audience, and the CFP's fields, word limits and selection criteria if published (paste them).
- [FORMAT] (optional; one of: lightning, talk, workshop; default: talk): The session format. Lightning is about 5 to 10 minutes, talk about 25 to 45 minutes, workshop a hands-on session of 1.5 hours or more.
- [SPEAKER_BACKGROUND] (optional): Your role, the experience that makes you credible on this topic, and previous talks, posts or projects.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Programme committees read hundreds of proposals and decide on most of them within the first few sentences. They accept talks that promise something specific and earned (a real system, a real failure, a number), fit the audience and track, and are clearly not a product pitch. They reject vague titles, abstracts that describe a topic instead of a talk, takeaways nobody could act on, and proposals that oversell what a 30-minute slot can deliver. Many CFPs review the abstract anonymously and use a separate private field for "why you" and the details that prove the talk is real.
</context>

<task>
Write a [FORMAT] proposal for this idea:
[TALK_IDEA]
Only if [CONFERENCE] was provided: 

Conference and CFP: [CONFERENCE]
Only if [SPEAKER_BACKGROUND] was provided: 

Speaker background: [SPEAKER_BACKGROUND]

1. Find the core: the one problem the audience has, the insight or experience that answers it, and the evidence (a production story, a measured result, a built thing). If the idea has no concrete experience or evidence behind it, say so and ask for it before writing; do not invent results, numbers, companies or anecdotes.
2. Write three title options: specific and searchable, saying what the talk delivers, under about ten words; one may be playful if the event suits it. Avoid clickbait and unexplained acronyms.
3. Write the abstract, within the CFP's word limit if given (otherwise 120 to 200 words for a talk, 60 to 100 for a lightning talk, 150 to 250 for a workshop). Open with the audience's problem or a concrete situation, then what the talk covers and the evidence, then what attendees will leave with. Write in the third person or neutral voice, and keep the speaker's name and employer out of it so it works for anonymous review.
4. Write the outline with timings that add up to the slot, including a short opening, the main sections, any demo (with a fallback if the demo fails) and time for questions. For a workshop, add prerequisites, setup to do before the session, the exercises and what each one teaches.
5. List three takeaways, each something an attendee can do or decide differently on Monday.
6. State the audience and level: who will get the most out of it, what they need to know already, and what the talk will not cover.
7. Write the notes for reviewers (the private field): why this speaker, where the story comes from, what is new compared with existing talks on the topic, whether it has been given before and what changed, links to supporting material (as placeholders), and that it is not a sales pitch if a vendor is involved.
8. Write a short speaker bio from the background given, in the third person, under 80 words. Skip it if no background was given and say so.
9. Check fit against the conference's audience, track and stated criteria, and list anything that may count against the proposal.
</task>

<constraints>
- Use only facts from the input. Placeholders such as [NUMBER] or [LINK] mark anything the speaker must fill in.
- No hype words ("revolutionary", "game-changing", "deep dive into everything") and no promises the timing cannot deliver.
- Match the conference's language conventions and limits if the CFP text is provided.
- Lead with the answer. Add reasoning only where it changes what the reader will do.
- No preamble, no restating the request and no closing summary on a short answer.
</constraints>

<output_format>
## Title options
Three numbered titles, the recommended one first.

## Abstract
The abstract, then its word count.

## Outline
Table: minutes | section | content. Timings sum to the slot.

## Takeaways
Three bullets.

## Audience and level
Two or three sentences.

## Notes for reviewers
A short paragraph or bullets.

## Speaker bio
The bio, or a note that background is needed.

## Fit check
Bullets: strengths for this event, and risks with a fix for each.
</output_format>
