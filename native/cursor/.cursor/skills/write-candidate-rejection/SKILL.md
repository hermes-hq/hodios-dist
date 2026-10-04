---
name: write-candidate-rejection
description: Writes respectful candidate rejection messages for each hiring stage, with optional specific feedback that is fair and legally careful. Use when closing the loop with applicants.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: hiring
  source: https://hermes-ide.com/prompts/write-candidate-rejection
  catalog: 2026.1004.0
---

# Write a candidate rejection

## Inputs

- [STAGE] (required; one of: application, phone-screen, take-home, interviews, final-round, offer-withdrawn): The stage the candidate reached.
- [CANDIDATE_NOTES] (optional): Optional details - candidate's first name, the role, what they did well, the main job-related reasons they were not selected (from the scorecard), whether you want to keep them in mind for future roles, and whether to offer a feedback call.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write candidate communications for recruiting teams that care about candidate experience. Being ignored is the most common complaint candidates have about hiring, and a clear, timely, kind rejection protects the employer's reputation and keeps good runners-up interested in future roles. The further a candidate went, the more personal the message should be: a short note at application stage; a personal email or call after interviews; specific feedback, when offered, that is honest, job-related and tied to the evidence. Feedback that is vague ("not the right fit"), personal ("not confident enough"), or that mentions protected characteristics creates legal and reputational risk.

Stage: [STAGE]
Only if [CANDIDATE_NOTES] was provided: 
<candidate_notes>
[CANDIDATE_NOTES]
</candidate_notes>
</context>

<task>
1. Write the message for the stage:
   - application: three to four sentences, thanking them, a clear decision in the first two sentences, and an optional line inviting them to apply for future roles.
   - phone-screen or take-home: a personal email that thanks them for their time and, for a take-home, for the effort, gives the decision clearly, and mentions one genuine strength if the notes give one.
   - interviews or final-round: a personal email (and a short call script if the notes ask for it) that acknowledges the time invested, gives the decision clearly and kindly, names one or two genuine strengths, offers specific feedback or a feedback call if the notes allow, and keeps the door open sincerely if they want to.
   - offer-withdrawn: a careful, direct message explaining the decision as far as can be shared, with an apology for the impact, and a recommendation to involve HR or legal before sending.
2. If feedback is included, write it from the job-related reasons in the notes: one or two specific, observable points tied to the role's criteria (for example "the panel looked for more experience leading stakeholder workshops, which the role requires from day one"), phrased constructively.
3. Feedback check: list the phrases you avoided or rewrote and why, and confirm the feedback contains nothing about protected characteristics, personality judgements or comparisons with other candidates.
4. Notes: suggested timing (as soon as the decision is final; within a few working days of the last interview), channel, and whether a call is better for later stages.
</task>

<constraints>
- State the decision clearly and early; do not bury it or give false hope ("we may reconsider") unless that is true.
- Never mention or hint at age, gender, pregnancy or family, disability or health, race, ethnicity, nationality, accent, religion, sexual orientation or other protected characteristics, and avoid proxies such as "overqualified", "culture fit", "energy" or "too senior for the team".
- Never invent reasons or strengths; use only the notes. If no job-related reason is given, write the message without specific feedback and suggest what to record from the scorecards first.
- Do not compare the candidate with the person hired or share other candidates' details.
- Keep it human, short and free of corporate clichés ("after careful consideration of your impressive background").
- If notes contain a reason that is discriminatory or legally risky, do not use it; flag it and recommend HR review the decision.
</constraints>

<output_format>
## Message
Subject line and body ready to send; call script if requested.
## Feedback check
## Notes
</output_format>
