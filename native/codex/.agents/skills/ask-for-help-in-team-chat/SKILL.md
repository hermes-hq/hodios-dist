---
name: ask-for-help-in-team-chat
description: Writes a question for a team chat channel that gets answered, with context, what was tried, the specific ask, urgency and where to reply. Use as a new hire or remote worker.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/ask-for-help-in-team-chat
  catalog: 2026.1003.2
---

# Ask for help in team chat

## Inputs

- [PROBLEM] (required): What you are trying to do, what is going wrong or what you do not know, with any error messages, links or screenshots described.
- [WHAT_WAS_TRIED] (optional): What you have already tried or checked, such as docs, searches, people asked or settings changed, and what happened.
- [URGENCY] (optional; one of: low, today, blocking; default: today): Low means it can wait days; today means you need an answer today; blocking means you cannot continue work until it is solved.
- [CHANNEL_AUDIENCE] (optional): Where you are posting and who reads it, for example "#it-help, the 3-person IT team" or "#eng-platform, about 60 engineers".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Questions in busy team channels get answered when a helper can understand them in one read and answer without a round of follow-ups. They go unanswered when they ask to ask ("anyone know about the VPN?"), describe an attempted fix instead of the goal (the "XY problem": asking how to do X when the real need is Y), leave out the error message or what was tried, or hide the urgency. A good question states the goal, what happened versus what was expected, what was tried, the specific question, and how urgent it is, in a short first message, with longer details in the thread. Posting the answer back afterwards turns the thread into documentation for the next person.
</context>

<task>
Write a team chat question.Only if [CHANNEL_AUDIENCE] was provided:  Channel and readers: [CHANNEL_AUDIENCE]. Urgency: [URGENCY].

<problem>
[PROBLEM]
</problem>
Only if [WHAT_WAS_TRIED] was provided: 
<what_was_tried>
[WHAT_WAS_TRIED]
</what_was_tried>

1. If you cannot tell what the person is trying to achieve, ask one question about the goal and stop.
2. Check for the XY problem: if the problem describes a workaround or a means, state the underlying goal first so helpers can suggest a better route.
3. Remove any secrets or sensitive data in the problem (passwords, API keys, tokens, customer personal data, financial account numbers) from the message, replace them with placeholders, and say so under Tips.
4. Main message, at most about five short lines:
   - The goal and the problem in one sentence.
   - Expected versus what actually happens, with the exact error text in a code span if there is one.
   - The specific question.
   - Urgency stated honestly: for "blocking", say what is blocked and since when; for "low", say it can wait.
   - Where to reply ("in thread, please").
5. Thread details: what was tried, environment or context (device, system, account, document link placeholders), and screenshots to attach, as a short list. Omit if there is nothing beyond the main message.
6. Tips: whether to tag a specific owner or team (only if the channel audience suggests one, and never tag a whole channel for a non-urgent question), and one line on searching the channel history first if that was not tried.
7. After it is answered: a one-line follow-up template that posts the solution and thanks the helper.
</task>

<constraints>
- Use only the facts given; never invent error messages, system names or steps tried. Use `[need: …]` where an error message or link would help.
- No "anyone around?", "quick question" or apology for asking.
- Do not inflate urgency; "blocking" only when the input says work cannot continue.
- Keep the tone friendly and matter-of-fact; suitable for a new joiner who does not know people yet.
</constraints>

<output_format>
## Main message
The message, ready to paste.
## Thread details
The thread reply, or "Not needed".
## Tips
Two or three bullets.
## After it is answered
One line.
</output_format>

<examples>
Weak: "Hey, does anyone know about the VPN?"
Strong: "I can't reach the staging dashboard from home: the VPN connects, but the page times out (`ERR_CONNECTION_TIMED_OUT`). Is there an extra step for staging access for new starters? Blocking my onboarding tasks since this morning. Details in thread 🧵"
</examples>
