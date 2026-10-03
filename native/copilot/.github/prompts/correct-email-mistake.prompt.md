---
description: Writes a short correction to a previous email or document, such as a wrong date, figure, attachment or recipient, that states the fix first, without drama or over-apology.
agent: agent
argument-hint: original_message mistake correction audience_size
---

# Correct a mistake in an email

<context>
A good correction is boring: a subject that says "Correction", the right information in the first line, enough of the wrong version that readers know what to discard, and at most one short apology. Corrections go wrong in three ways. Over-apologising turns a typo into an incident and makes the sender look shaken. Burying the fix in a paragraph means half the readers still act on the wrong date. And not every mistake deserves a correction: a typo that changes no meaning creates more noise than it fixes. Some mistakes are not just errors but incidents: personal or confidential data sent to the wrong people usually has to be reported inside the organisation (often to a data protection or security contact) quickly, and the recipients asked to delete it. Email recall rarely works reliably and should not be relied on.
</context>

<task>
Write a correction for a ${input:audience_size:Who received the original. One-person and small-group corrections can be more personal; large-list corrections must be scannable and impossible to misread.} audience.

<original_message>
${input:original_message:The email or announcement that contained the mistake, pasted in full or at least the part with the error and its subject line.}
</original_message>

<mistake>
${input:mistake:What was wrong, for example "date says Wednesday 13 Nov, should be Thursday 14 Nov" or "sent the salary spreadsheet to the whole team instead of to HR".}
</mistake>

<correction>
${input:correction:The correct information or the fix, for example the right figure, the right attachment, or what you want recipients to do.}
</correction>

1. Decide whether a correction is worth sending. Recommend not sending one when the mistake is a typo or wording slip that changes no fact, action, amount or date, and say why in one line. Otherwise continue.
2. Classify the mistake: wrong fact (date, time, amount, link, name), wrong or missing attachment, wrong recipient, or confidential or personal data exposed. Base the rest on the class.
3. Write the correction:
   - Subject: "Correction: [original subject]" (or "Updated attachment: …"). For a single recipient, a reply in the same thread is fine.
   - First line: the correct information, stated so it cannot be misread, with the wrong version named once so readers know what to discard ("The workshop is on Thursday 14 Nov, not Wednesday 13 Nov as I wrote earlier.").
   - Any action readers must take: update the calendar, use the new link, discard the old file.
   - Apology: none needed for a small factual slip to a large list beyond "apologies for the confusion"; one plain sentence otherwise. Never more than one.
   - For a wrong recipient or exposed data: ask the recipients not to open, forward or save the material and to delete it (and confirm they have, for sensitive data), without repeating the sensitive content.
4. For a large list, make the corrected fact bold or put it on its own line, and keep the email to three or four lines.
5. Under "Also do", list practical follow-ups: send an updated calendar invite, fix the source document or web page, tell people who might have acted on the wrong information, and for exposed personal or confidential data, report it to the organisation's data protection, privacy or security contact straight away because reporting deadlines can be short.
</task>

<constraints>
- Correction body under about 80 words (under about 50 for one-person corrections).
- Use only the facts given; never invent the right value if the correction is unclear, ask instead.
- No drama: no "huge apologies", "mortified", or explanations of how the mistake happened unless the reader needs it to act.
- Never repeat personal or confidential data in the correction itself.
- Do not claim the email was recalled.
</constraints>

<output_format>
## Send a correction?
One or two sentences with the recommendation.
## Correction
Subject line, then the body. Omit if not recommended.
## Also do
Bullets. "Nothing else" if none.
## Notes
Placeholders and assumptions. "None" if nothing.
</output_format>
