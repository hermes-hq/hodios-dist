---
name: ask-for-feedback-by-email
description: Writes a request for feedback on a piece of work, a talk or your own performance, with two or three specific questions and an easy format, so people actually answer.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/ask-for-feedback-by-email
  catalog: 2026.1003.2
---

# Ask for feedback by email

## Inputs

- [WORK_OR_TOPIC] (required): What you want feedback on and its stage, for example "draft of the Q3 board deck, structure is final, wording is not" or "my facilitation of the last three retros".
- [RECIPIENT_RELATIONSHIP] (required): Who you are asking, for example "my manager", "a peer on another team", "two senior engineers I barely know" or "workshop attendees".
- [DEADLINE] (optional): When you need the feedback, and why if it helps, for example "Thursday, before I send it to the board".
- [FORMAT] (optional; one of: email-reply, short-call, form; default: email-reply): How they will respond. Email-reply means numbered answers by email; short-call means a 15-minute chat; form means a short anonymous or named form you will send.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
"Any feedback?" gets "looks good" or silence. People give useful feedback when the request tells them what stage the work is in, what kind of feedback is wanted (direction, structure or line edits), asks two or three specific questions tied to decisions the sender is actually making, makes it safe to be critical ("the most useful thing is what you would cut"), takes a stated small amount of time, and has a deadline. Performance feedback works best with a narrow, behavioural question ("what is one thing I could do differently in planning meetings?") rather than "how am I doing?". Peers and people further down the hierarchy need explicit permission and sometimes anonymity to be candid.
</context>

<task>
Write a feedback request to [RECIPIENT_RELATIONSHIP] in the [FORMAT] format.Only if [DEADLINE] was provided:  Needed by: [DEADLINE].

<work_or_topic>
[WORK_OR_TOPIC]
</work_or_topic>

1. If you cannot tell what the feedback is about (for example "my stuff" or "everything"), ask what specifically and stop.
2. Identify the decisions or uncertainties the sender most likely has at this stage, from the work and its stage, and write two or three specific questions. At least one must invite criticism directly (what to cut, what is unclear, what they would do differently). Avoid yes/no questions and "did you like it".
3. State what kind of feedback is not needed now (for example "no need for typos; wording changes next week"), when the stage makes that clear.
4. Write the request:
   - Subject: "[Topic]: 3 quick questions, by [date]" or similar, with the time needed.
   - First line: what you are asking for and how long it takes ("10 minutes").
   - One or two lines of context and the stage.
   - The questions (numbered for email-reply; as an agenda for short-call; as a link placeholder with the questions listed for form).
   - Permission to be candid, fitted to the relationship: for a manager, ask directly; for peers or people more junior, make it clearly safe and offer the anonymous form option if the format allows.
   - Deadline and thanks; promise to share what you change, which makes people more likely to answer next time.
5. For performance feedback, keep questions behavioural and forward-looking, about specific situations named in the input.
</task>

<constraints>
- Under about 120 words in the body, excluding the questions.
- Two or three questions; never more than three in email-reply or short-call; a form may add one optional rating question.
- Use only the context given; never invent details of the work or past events. Use `[need: …]` for links and dates.
- No fishing for praise and no self-deprecation ("it's probably terrible").
- Plain, friendly and specific to the relationship; no HR jargon.
</constraints>

<output_format>
## Email
Subject line, then the body.
## Questions
The questions alone, ready to paste into a form or doc, each with a one-line note on what decision it informs.
## Notes
How to receive the feedback well (one or two lines), placeholders, and who else might be worth asking. "None" if nothing.
</output_format>

<examples>
Weak: "Would love any feedback you have on the deck!"
Strong: "1. Is the recommendation on slide 3 clear without me presenting it? 2. Which slide would you cut if we only had 10 minutes? 3. Is anything here likely to surprise the CFO?"
</examples>
