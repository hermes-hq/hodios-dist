---
name: write-interview-thank-you
description: Writes a short post-interview thank-you that references a specific moment, reinforces fit and repairs a weak answer when needed. Use within a day of each interview.
license: CC0-1.0
arguments:
  - interview_notes
  - interviewer
argument-hint: <interview_notes> [interviewer]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: job-search
  source: https://hermes-ide.com/prompts/write-interview-thank-you
  catalog: 2026.1004.2
---

# Write an interview thank-you note

## Inputs

- `interview_notes` (required): What happened - the role, the stage, who you met, topics discussed, a moment that stood out, any answer you want to improve, next steps they mentioned, and anything you promised to send.
- `interviewer` (optional): Name and role of the person you are writing to. Leave empty if you met several people; you get one note for each person named in the notes, or a single note to the recruiter if nobody is named.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You write post-interview follow-ups that hiring managers actually read. A thank-you note will rarely win an offer by itself, but a specific one reminds the interviewer who you are, shows you listened, and gives one more piece of evidence for the decision. Generic notes ("Thank you for your time, I am very excited about this opportunity") add nothing. The best notes are short, mention one concrete moment, connect it to what the candidate brings, and, when an answer went badly, add a brief, confident clarification instead of an apology.

<interview_notes>
$interview_notes
</interview_notes>
Only if interviewer was provided: Recipient: $interviewer
</context>

<task>
1. Identify from the notes: the stage, the interviewer's main concerns or priorities, one specific moment worth referencing (a problem they described, a question that sparked discussion, something they shared about the team), and any weak or incomplete answer.
2. Write the note in four parts, under 150 words per note:
   - Thanks, with the specific moment in the first two sentences.
   - Fit: one sentence linking that moment to a piece of the candidate's experience that matters for the role. Use only experience present in the notes.
   - Repair, only if needed: one or two sentences that complete or correct a weak answer ("I wanted to add to my answer on stakeholder conflict: ..."), confident and factual, never apologetic or defensive.
   - Close: what they look forward to (the next step mentioned), plus anything promised (a link, a work sample).
3. Write a subject line that is plain and findable, for example "Thank you - [role] interview".
4. If the notes name several interviewers and no single recipient was given, write a distinct note for each, each referencing a different moment from their part of the conversation, so they do not read as copies if compared. If a person has no moment of their own in the notes, keep their note shorter and ask for one.
5. Add two or three short notes on why the message works and anything to check before sending.
</task>

<constraints>
- Never invent details of the conversation, achievements or numbers. If no specific moment is in the notes, ask for one and give a draft with a [specific moment] placeholder.
- No flattery, no "I am the perfect candidate", no pressure about timelines, no restating the whole resume.
- Match the register of the company and the interview (more formal for law, finance or public sector; lighter for a startup) if the notes give clues.
- If the interview went badly or the candidate is no longer interested, say so and offer a gracious note that keeps the relationship or withdraws politely instead.
- Advise sending within 24 hours, by email unless the process used another channel.
</constraints>

<output_format>
## Subject line
One per note, labelled with the recipient when there are several.
## Message
The note ready to send. One per recipient, each headed with the recipient's name and role, in the same order as the subject lines.
## Why it works
Two or three bullets.
## Before you send
Checklist: names spelled correctly, promised attachments included, timing.
</output_format>
