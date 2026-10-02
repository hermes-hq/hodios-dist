---
name: write-introduction-email
description: Writes a double opt-in introduction, first the private ask to the person being introduced, then the intro email itself, with why the two should talk and an easy next step.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/write-introduction-email
  catalog: 2026.1002.2
---

# Write an introduction email

## Inputs

- [PERSON_A] (required): The first person (usually the one who asked for the intro, or the one with the ask), with their role, what they want or offer, and how you know them.
- [PERSON_B] (required): The second person, usually the busier one, with their role, interests and how you know them.
- [REASON] (required): Why they should talk, specifically, and what a good outcome would be for each of them.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A double opt-in introduction asks the busier or more senior person privately whether they want the intro before connecting them. It protects the connector's relationships and makes the eventual intro warmer, because both people have agreed. Good introductions are short and specific: who each person is in one line, why they in particular should talk, what is in it for the person being asked, and an easy next step that puts the burden on the person who asked. Weak ones are vague ("you two should connect!"), forward a long thread, or obligate a busy person in public.
</context>

<task>
Write a double opt-in introduction.

<person_a>
[PERSON_A]
</person_a>

<person_b>
[PERSON_B]
</person_b>

<reason>
[REASON]
</reason>

1. If it is unclear who is asking for what, or why person B would want this, ask one or two short questions and stop.
2. Decide who needs to opt in (usually the busier person, or whoever is being asked for something; both when the intro would reveal something sensitive about either, such as a confidential job search). Say which and why in Notes.
3. Write a private opt-in request to each person who needs to opt in: two to five sentences naming who the other person is, the specific reason they might want to talk, what is being asked of them (time, advice, a meeting), and an easy way to decline ("No worries at all if the timing isn't right"). Suggest the person who asked for the intro supplies a forwardable blurb.
4. Write the introduction email, to be sent once both agree: a subject line with both names, one line on each person (what they do and why relevant to the other), the specific reason for the intro, and a clear next step, usually that the person who asked will follow up with times. Suggest moving the connector to BCC.
5. Write a two-sentence forwardable blurb for each person in case either needs it.
</task>

<constraints>
- Specific and brief: each email under about 150 words. No gushing superlatives.
- Use only the facts given about each person; do not invent titles, companies or achievements.
- Never imply someone has already agreed when they have not.
- Do not share private details about one person with the other unless the brief says it is fine.
- Put the effort on the person who benefits most: they schedule, they follow up.
</constraints>

<output_format>
## Opt-in request
One per person who needs to opt in: To: [name]. Subject line and the message.
## Introduction email
Subject line and the message, to send once both agree.
## Blurbs
Person A: two sentences. Person B: two sentences.
## Notes
Who should opt in and why, and any detail to confirm before sending.
</output_format>
