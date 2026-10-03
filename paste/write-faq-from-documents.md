<context>
A good FAQ answers the questions people actually have, in the words they would use, so they stop emailing the organiser. Most FAQs fail because they are written from the document's structure instead of the reader's situation ("What is the scope of the policy?" instead of "Can I work from abroad for two weeks?"), because answers are padded or vague, or because they quietly paper over places where two source documents disagree. When the answer is wrong, the FAQ does more damage than no FAQ, so every answer must trace back to a source, and anything the sources do not settle must be visible to the owner, not guessed.
</context>

<task>
Build an FAQ for this audience: [AUDIENCE]. Include at most 15 questions.

<source_material>
[SOURCE_MATERIAL]
</source_material>

1. If there is no usable source material, ask for it and stop. If the sources are unlabelled, label them S1, S2, … in the order given and use those labels throughout.
2. Imagine the reader's real situations: before, during and after the thing the sources cover, and what goes wrong. List the questions they would ask, phrased in their words (first person, plain language, specific: "What if my flight is cancelled?" not "Flight disruption procedures").
3. Rank them by how many readers will ask and how costly a wrong guess would be (money, deadlines, safety, eligibility). Keep the top 15; note the rest under Gaps as "not included".
4. Answer each from the sources only:
   - Lead with the direct answer (yes, no, the number, the deadline), then the condition or exception, then what to do or whom to contact.
   - Quote exact figures, dates and limits as written in the source.
   - End the answer with its source label(s) in brackets, for example "[S2]".
   - If a source answers only part of the question, answer that part and say what is not covered.
5. Where two sources disagree, do not choose silently. Give the most recent or most authoritative answer only if the sources make the order clear, and list every disagreement under Conflicts.
6. Questions the audience will clearly ask but the sources do not answer go under Gaps with a suggested owner to answer them. Do not include them in the FAQ with an invented answer.
7. Group the questions under three to six short headings in the order the reader will need them.
</task>

<constraints>
- No answer may contain a fact that is not in the sources. Plausible-sounding policy details are the main risk here.
- Answers under about 80 words each; link or point to the source for the full detail.
- Plain language: second person ("you"), active voice, no internal jargon unless the audience uses it.
- Do not reproduce personal data from the sources (names, phone numbers, personal emails) unless it is clearly meant as a public contact point.
</constraints>

<output_format>
## FAQ
Grouped questions as `### Heading` then `**Question?**` followed by the answer and source label.
## Source map
Table: Source label · Source title or description · Questions it answers.
## Conflicts
Bullets: the question, what each source says (with labels), and who should resolve it. "None found" if none.
## Gaps
Bullets: questions readers will ask that the sources do not answer, plus any questions cut by the limit, each with a suggested owner. "None" if none.
</output_format>

<examples>
Weak: **What is the expense policy for meals?** Meals are reimbursed in line with company policy.
Strong: **How much can I spend on dinner when I travel?** Up to 40 EUR per person per day, including tips. Alcohol is not reimbursed. Keep the itemised receipt and submit it within 30 days. [S1]
</examples>
