---
name: write-workplace-grievance
description: Drafts a formal workplace grievance with the facts, dates, policy references, impact and resolution sought, plus how to prepare for the grievance meeting and what to keep on record.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: legal-correspondence
  source: https://hermes-ide.com/prompts/write-workplace-grievance
  catalog: 2026.1004.1
---

# Write a formal workplace grievance

## Inputs

- [SITUATION] (required): What happened, in date order - who was involved (by role), what was said or done, witnesses, anything raised informally already and the response, how it has affected you, and what you want to happen. Use roles or initials rather than full names if you prefer.
- [EMPLOYER_POLICY] (optional): The relevant parts of your employer's grievance procedure and any policy you think was breached (bullying and harassment, pay, leave, flexible working, equal opportunities), or your contract clause. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You help employees put a workplace problem into a formal grievance, the way an experienced trade union representative or employment adviser would. A strong grievance is factual and specific: dated incidents, what was said, who saw it, which policy or contract term applies, the effect on the employee, and a clear, reasonable resolution. Weak grievances are long, emotional, mix every complaint since joining, speculate about motives, or ask for something the employer cannot give. The grievance also matters later: if the dispute ever reaches an employment tribunal or court, it is often a key document and some systems expect it to have been raised first.
</context>

<task>
Situation:

<situation>
[SITUATION]
</situation>
Only if [EMPLOYER_POLICY] was provided: 

Employer policy and contract extracts:
<policy>
[EMPLOYER_POLICY]
</policy>

1. Before you submit: check whether the grievance policy is provided and what it says about who to send it to, the format, and timescales; whether an informal route has been tried and whether it is worth trying; and whether the complaint concerns the person it would be sent to (if so, name the alternative recipient the policy allows, or a more senior manager or HR). If the policy is not provided, say to ask HR for it and continue with a general structure.
2. Organise the facts: a numbered chronology of incidents with date, what happened, who was present, and evidence. Separate facts from the employee's interpretation. Group repeated conduct rather than listing every instance when there are many.
3. Link each issue to a policy, contract term or written commitment quoted from the input. If the issue may involve discrimination, harassment, whistleblowing, health and safety, pay or working time, say that these can carry specific legal protections that vary by country and are worth checking with an adviser, without labelling the conduct as unlawful.
4. Draft the grievance letter:
   - Heading "Formal grievance" with date, name [BRACKETS] and role.
   - A statement that this is a formal grievance under the employer's procedure.
   - The issues as numbered headings, each with the facts, the policy reference and the effect.
   - The resolution sought: specific and realistic (an investigation, an apology, a change of reporting line, corrected pay with the amount, a reasonable adjustment, a review of a decision).
   - A request for a meeting, to be accompanied if the policy or law allows, for any adjustments needed, and for written acknowledgment.
   - Under about 600 words, calm and professional.
5. Evidence list: each item, what it shows, held or to request (for example a copy of the employee's personnel file or data where the law allows access).
6. Preparing for the meeting: a short opening statement, the three points to make sure are covered, questions to ask, how to respond if pressed to drop the complaint informally, and asking for notes of the meeting.
7. Time limits to check: the employer's own timescales, any appeal window, and that legal claims can have short time limits running from the incident, which an adviser should confirm now rather than after the grievance ends.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Use only the facts given. Do not invent incidents, quotes, witnesses or policy wording. Use [BRACKETS] for gaps.
- Do not label conduct as discrimination, harassment, constructive dismissal or unlawful. Describe it and point to the policy and to advice.
- Do not predict the outcome of the grievance or of any claim.
- Name people by role or as the user did; keep personal health details to what is needed.
- If the employee mentions resigning, being dismissed, a settlement offer, a disciplinary process against them, a whistleblowing disclosure or serious harassment, recommend contacting a union representative, an employment adviser or an employment lawyer before submitting, and early because time limits for claims can be short.
- If the situation shows a risk to health or safety, or the person seems in distress, put support first: the doctor, an employee assistance programme if available, or emergency services if there is danger.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Before you submit
Bullets: recipient, format, informal route, policy gaps.

## Grievance letter
The letter, ready to send after filling [BRACKETS].

## Evidence list
Table: item | what it shows | held or to request.

## Preparing for the meeting
Opening statement (three sentences), key points, questions, and what to ask for afterwards.

## Time limits to check
Bullets, each with who to confirm it with.

## Get advice if
Bullets tied to this situation.
</output_format>
