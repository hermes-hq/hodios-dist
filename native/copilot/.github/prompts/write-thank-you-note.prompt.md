---
description: Writes a specific, heartfelt thank-you note that names what the person did, the detail that showed care and why it mattered, for cards, emails and post-interview notes.
agent: agent
argument-hint: recipient what_they_did tone
---

# Write a thank-you note

<context>
A thank-you note is remembered for one specific detail. Generic notes ("Thanks so much for everything, it really meant a lot!") could be sent to anyone and feel like it. A good note names exactly what the person did, notices the effort or care behind it, says what difference it made, and, where natural, looks ahead. Post-interview notes have their own conventions: sent within a day, brief, referencing something specific from the conversation and restating interest, with no pressure.
</context>

<task>
Write a ${input:tone:Warm for friends, family and close colleagues; formal for interviewers, senior contacts or official thanks.} thank-you note to ${input:recipient:Who you are thanking and your relationship, for example "my aunt", "a mentor I've had coffee with twice", "the interviewer for a product role".} for this:
<what_they_did>
${input:what_they_did:What they did, any specific detail you remember, and what difference it made to you. The more concrete, the better the note.}
</what_they_did>

1. If the input says only "thanks for everything" or similar, with no specific action, ask what they did and one detail you remember, and stop.
2. Open by thanking them for the specific thing, not with "I just wanted to say".
3. Name the detail that shows you noticed their effort or thought, taken from the input.
4. Say what difference it made to you (or your family, team or project), concretely.
5. Close warmly with a look ahead that fits the relationship (looking forward to seeing them, putting the advice into practice, a return favour) only where the input makes it natural.
6. For an interview thank-you: thank them for their time, reference one specific topic from the conversation, restate interest in the role in one sentence, and offer to provide anything else; no recap of your CV.
7. Length: 50 to 120 words for a card or email; under 40 for the shorter version.
</task>

<constraints>
- Use only details from the input. If the note would be stronger with a detail you do not have, put a `[detail: …]` placeholder and list it under Details to add.
- No gushing superlatives stacked together, no clichés ("words cannot express"), and no more than one exclamation mark.
- Formal tone: full sentences, no contractions or emoji. Warm tone: personal and natural, as you would write by hand.
- Do not mention gifts' prices or compare gifts.
</constraints>

<output_format>
## Note
The note, with greeting and sign-off.
## Shorter version
For a text message or a small card.
## Details to add
Any placeholders and what would fill them. "None" if none.
</output_format>
