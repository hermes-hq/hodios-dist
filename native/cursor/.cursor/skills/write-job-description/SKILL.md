---
name: write-job-description
description: Writes an inclusive job description built on outcomes, a short list of true must-haves versus trainable skills, and an honest view of the role's challenges. Use when opening a new role.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: hiring
  source: https://hermes-ide.com/prompts/write-job-description
  catalog: 2026.1002.2
---

# Write a job description

## Inputs

- [ROLE] (required): The job title you have in mind.
- [TEAM_CONTEXT] (required): The team and why you are hiring - what this person will own, the problems to solve in the first year, who they work with, work mode and location, pay range, and anything hard about the role.
- [LEVEL] (optional): Seniority (for example junior, mid, senior, lead) or your internal level. Optional; inferred from the context if not given.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a hiring lead who writes job descriptions that attract the right people and help the wrong ones self-select out. Most job descriptions are a list of duties and a long wish list of requirements. Long requirement lists shrink and skew the applicant pool, because many qualified people, often women and people from under-represented groups, apply only when they meet nearly every item. Inflated years-of-experience and degree requirements screen out capable people without predicting performance. A strong description says what success looks like, separates the few true must-haves from what can be learned on the job, and is honest about the hard parts.

Role: [ROLE]
Only if [LEVEL] was provided: Level: [LEVEL]

<team_context>
[TEAM_CONTEXT]
</team_context>
</context>

<task>
1. Define the outcomes: 3-5 things this person will achieve in the first 6-12 months, written as results (for example "Cut invoice processing time in half by redesigning the approval flow"), drawn from the context.
2. Sort the requirements: at most 5 must-haves that someone truly cannot do the job without on day one, and a list of skills that can be learned in the first months. Replace years-of-experience counts with the capability they stand for where possible, and make degrees optional unless legally or professionally required.
3. Write the job description:
   - Title: a clear, searchable title that matches the level; no "ninja", "rockstar" or internal jargon.
   - Opening (3-4 sentences): the team, the mission, and why the role exists now.
   - What you will achieve: the outcomes.
   - What you will do day to day: 4-6 bullets.
   - What you need: the must-haves.
   - Nice to have / we will help you learn: the trainable list, with an explicit invitation to apply without meeting every item.
   - The honest part: 1-3 real challenges (for example legacy systems, ambiguity, travel, on-call).
   - Pay, benefits, work mode, location and the hiring process with its stages and timeline.
   - An accessibility and adjustments statement and an equal-opportunity statement.
4. Run an inclusion check: flag gender-coded or exclusionary wording (for example "aggressive", "dominant", "digital native", "young and energetic", "native English speaker" where fluency is meant), unnecessary physical requirements, and jargon, and show the replacement used.
</task>

<constraints>
- Use only facts from the context; mark unknowns, such as the pay range, as [placeholder] and list them under Open questions. Some jurisdictions require pay ranges in postings; remind the user to check local rules.
- 400-700 words for the description. Second person ("you"), plain language.
- Never include requirements related to age, gender, family status, nationality, religion, health or other protected characteristics, and avoid proxies for them.
- Do not overstate perks or culture; describe what is true.
</constraints>

<output_format>
## Job description
Ready to post.
## Must-haves versus trainable
Table: Requirement | Must-have or trainable | Why.
## Inclusion check
Table: Original or risky wording | Replacement | Reason.
## Open questions
</output_format>
