---
name: write-public-consultation-response
description: Writes a response to a government or regulator public consultation that answers the published questions in order, states the respondent's position with evidence and proposes concrete changes.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/write-public-consultation-response
  catalog: 2026.1003.1
---

# Write a public consultation response

## Inputs

- [CONSULTATION_QUESTIONS] (required): The consultation's numbered questions as published, plus the title, the body running it, the deadline, any word limits and the key proposals they refer to.
- [RESPONDENT_POSITION] (required): Who is responding (an individual, a business, a charity, an association and who it represents), what you support, what you oppose and what you want changed.
- [EVIDENCE] (optional): Facts, figures, cases, research and member experiences you can cite, with sources. Mark anything confidential.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Officials who analyse consultation responses usually code them question by question, often in a spreadsheet, counting positions and extracting evidence and specific proposals. A response has influence when it is easy to code (it answers each numbered question under that number, with a clear position), when it brings evidence the officials do not already have (data, costs, real cases, the experience of the people the respondent represents), and when it proposes a specific, workable change to the text or design of the proposal. Responses that restate the respondent's general views, attack motives, ignore the questions, or overstate evidence are discounted, and identical campaign letters are typically counted once.
</context>

<task>
Draft a consultation response.

<consultation_questions>
[CONSULTATION_QUESTIONS]
</consultation_questions>

<respondent_position>
[RESPONDENT_POSITION]
</respondent_position>
Only if [EVIDENCE] was provided: 
<evidence>
[EVIDENCE]
</evidence>

1. If the questions are missing, or you cannot tell what the respondent wants, ask for them and stop.
2. Write a short respondent statement: who is responding, whom they represent and how many, their relevant experience, and any interest to declare. Use placeholders for details not supplied.
3. Write a summary of the response in four to six bullets: the overall position and the most important changes sought.
4. Answer every question under its own number and wording, in order:
   - Start with a clear position where the question invites one (Agree, Disagree, Partly agree, Do not know, or the answer options the consultation gives).
   - Give the reasons, most important first, each supported by evidence from the input with its source.
   - Describe the practical impact on the people the respondent represents (costs, time, risks, unintended consequences), quantified where the evidence allows.
   - Propose a specific change: revised wording, a threshold, a transition period, an exemption or an alternative mechanism. Say what problem the change solves.
   - Acknowledge the policy aim and any trade-off honestly; officials discount responses that pretend there is none.
   If the respondent has no view or evidence on a question, write "No response" rather than padding.
5. Respect word limits per question or overall; if the evidence will not fit, prioritise the questions most central to the respondent's position and say which were shortened.
</task>

<constraints>
- Use only the evidence supplied. Never invent statistics, studies, cases, quotes or legal references. Where a claim would need evidence that is not given, mark it `[evidence needed: …]`.
- Distinguish data from anecdote and from opinion in the wording ("in a survey of 212 members, 64% said…" versus "several members told us…").
- Respectful and precise; no attacks on officials or other stakeholders.
- Responses are often published. Flag anything in the input marked confidential or that identifies individuals, and keep it out of the main response unless the user says otherwise.
- This is drafting help, not legal advice. If the proposal has legal consequences for the respondent, note that a legal adviser should review the position before submission.
</constraints>

<output_format>
## Response
Respondent statement · Summary · Answers by question number (heading = number and question text).
## Evidence used
Table: Claim · Question number · Source from the input · Type (data, case, expert view, member experience).
## Gaps and risks
Bullets: `[evidence needed: …]` items, questions left unanswered, possible weaknesses officials may probe, confidentiality flags, and the deadline and submission route if given.
</output_format>
