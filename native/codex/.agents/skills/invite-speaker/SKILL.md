---
name: invite-speaker
description: Writes an invitation to a speaker, guest expert or panelist with why them, the audience, the format, date options, what is offered and an easy reply path. Use for events, podcasts and classes.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/invite-speaker
  catalog: 2026.1004.3
---

# Invite a speaker

## Inputs

- [SPEAKER] (required): Who you are inviting and why them specifically, such as a talk, book, article or project of theirs that fits, and how you know them (or that you do not).
- [EVENT] (required): The event, podcast or class, the organiser, the format (keynote, panel, fireside chat, interview, guest lecture), length, in person or remote, and the topic you want them to cover.
- [AUDIENCE] (required): Who will be listening and how many, for example "120 operations managers from mid-size manufacturers" or "about 2,000 podcast listeners per episode".
- [OFFER] (optional): What you offer, such as fee or honorarium, travel and hotel, recording, promotion, or that it is unpaid. Being upfront here gets faster answers.
- [DATES] (optional): The date or date options, with time zone, and when you need an answer.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Speakers and guest experts receive many invitations and decide in seconds based on four things: is this for me specifically, is the audience worth my time, what exactly would I be doing and when, and what do I get. Invitations get ignored when they open with a long description of the organisation, flatter generically ("we love your work"), hide whether it is paid, leave out the time commitment (preparation, travel, the slot itself), or make replying hard. Strong invitations name the specific piece of the speaker's work that fits, describe the audience concretely, state the format, length and dates, are upfront about money and logistics, say what the organiser will handle, and close with a simple yes, no or "tell me more" path. For well-known people, the invitation often goes through an agent or assistant and must contain everything they need to put it in front of the speaker.
</context>

<task>
Write a speaker invitation to [SPEAKER].

<event>
[EVENT]
</event>
Audience: [AUDIENCE]
Only if [OFFER] was provided: 
<offer>
[OFFER]
</offer>
Only if [DATES] was provided: 
Dates: [DATES]

1. If the event's format or topic is unclear, or nothing is said about why this speaker, ask up to two questions and stop.
2. If the input suggests the speaker is booked through an agent, bureau or assistant, address it to them, keep it factual and complete, and make it easy to forward.
3. Subject: "[Invitation]: speak on [topic] at [event], [date or month]".
4. Opening: the invitation in one sentence, and why them in one or two sentences tied to their specific work as given. If the input gives no specific work, use `[need: their talk, article or project that fits]` rather than generic praise.
5. The audience: who, how many, and what they want to leave with.
6. The ask: format, length, topic or angle (with room for them to shape it), in person or remote, and the total time commitment including any prep call or rehearsal.
7. Dates: the options with time zone, and the date you need an answer by.
8. The offer: fee or honorarium, travel and accommodation, recording and how it will be used, promotion. If unpaid, say so plainly and state what is offered instead, without calling it "exposure".
9. What the organiser handles (AV, moderation, tech check, questions in advance) only as given or as placeholders.
10. Reply path: a one-line yes, no, or "happy to talk", plus a short call offer. An easy decline ("if the timing doesn't work, a recommendation of someone else would be welcome") is optional and short.
11. Write a short version (under about 70 words) for LinkedIn or a DM.
12. Under "Have ready", list what to send once they accept: event brief, speaker form, bio and headshot request with deadline, run of show, recording consent.
</task>

<constraints>
- Email body under about 200 words.
- Use only facts given; never invent audience figures, fees, past speakers, sponsors or the speaker's work. Use `[need: …]`.
- Specific, warm and professional; no gushing, no "huge fan", no pressure tactics or false scarcity.
- State money clearly in the first half of the email if it is unpaid or if the fee is a key detail.
- If a recording will be published or reused, say so in the invitation, not after acceptance.
</constraints>

<output_format>
## Email
Subject line, then the body.
## Short version
The short message.
## Have ready
Bullets.
## Notes
Placeholders and any facts to confirm. "None" if nothing.
</output_format>
