---
name: write-cover-letter
description: Writes a tailored cover letter under 350 words that connects two or three specific achievements to the role's most important needs. Use for any job application that asks for one.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: job-search
  source: https://hermes-ide.com/prompts/write-cover-letter
  catalog: 2026.1002.2
---

# Write a cover letter

## Inputs

- [JOB_POSTING] (required): The full job posting text, plus anything you know about the team or company that the letter could reference.
- [RESUME] (required): Your resume, or notes on the achievements you want to draw from.
- [TONE] (optional; one of: formal, warm, direct; default: direct): Register of the letter. formal suits law, finance and public sector; warm suits mission-driven and small teams; direct suits most tech and business roles.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a hiring manager who has read thousands of cover letters and remembers almost none of them. The forgettable ones restate the resume, open with "I am writing to apply for", and claim traits ("passionate", "detail-oriented") without proof. The ones that get a candidate an interview answer one question fast: "Can this person solve the problem we are hiring for?" They do it with two or three specific achievements chosen for this role, in the candidate's own voice.

<job_posting>
[JOB_POSTING]
</job_posting>

<resume>
[RESUME]
</resume>

Tone: [TONE]
</context>

<task>
1. Identify the two or three needs that matter most to this hiring manager: the problems in the responsibilities, not the generic requirements.
2. For each need, pick the single strongest piece of evidence from the resume: an achievement with action, scope and result. Prefer evidence that is close to the role's context (same kind of user, scale, industry or problem).
3. Write the letter:
   - Opening (2-3 sentences): name the role, then lead with the strongest match or a specific, true reason for wanting this role at this company. No "I am writing to apply".
   - Body (one short paragraph per need, or a tight paragraph plus 2-3 bullets): need, evidence, result, and what it means for them.
   - If there is an obvious question (career change, gap, relocation, overqualification), answer it in one confident sentence. Do not apologise.
   - Close (1-2 sentences): what you would bring in the first months and a plain call to talk.
4. Match the tone: formal (complete sentences, no contractions, restrained), warm (personal motivation, connection to the mission), direct (short sentences, lead with results).
</task>

<constraints>
- Under 350 words for the letter body. Shorter is better if it is complete.
- Use only facts in the resume. Never invent metrics, employers, tools or motivations. If a strong letter needs a fact you do not have (the hiring manager's name, why this company, a number), write a [placeholder] and list it under "Check before sending".
- Do not repeat the resume line by line; select and connect.
- Mirror two or three of the posting's key terms naturally, without keyword stuffing.
- No clichés: "passionate", "team player", "hit the ground running", "perfect fit", "I believe I would be a great asset".
- Address "Dear Hiring Manager" unless a name is given; when none is, add "find the hiring manager's name" to Check before sending rather than a name placeholder in the salutation. Sign off with [Your name].
</constraints>

<output_format>
## Letter
The full letter, ready to paste.
## Why these choices
Three bullets at most: which needs you targeted and which evidence you used for each.
## Check before sending
Bullets: every [placeholder] to fill and any claim the candidate should verify.
</output_format>
