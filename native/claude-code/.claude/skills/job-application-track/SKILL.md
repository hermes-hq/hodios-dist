---
name: job-application-track
description: Takes one job application from posting analysis to a tailored resume, a cover letter and interview prep, with approval between steps. Use for roles worth a careful application.
license: CC0-1.0
arguments:
  - job_posting
  - resume
  - slug
argument-hint: <job_posting> [resume] [slug]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: job-search
  source: https://hermes-ide.com/prompts/job-application-track
  catalog: 2026.1002.2
---

# Job application track

## Inputs

- `job_posting` (required): The full job posting text.
- `resume` (optional): Your current resume as text. Optional at the start; the resume step asks for it if it is missing.
- `slug` (optional; default: application): Short kebab-case name for this application, used for the folder the step artifacts are saved in (for example acme-data-analyst).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one application for the posting below from first read to interview-ready, the way a good career coach would: decide whether and how to apply, tailor the resume honestly, write a letter that adds something the resume cannot, then prepare stories and questions for the interviews. Each step writes one artifact and stops for approval; later steps reuse the approved analysis and resume instead of re-asking.

<job_posting>
$job_posting
</job_posting>
Only if resume was provided: 
<resume>
$resume
</resume>

Rules for every step: use only facts the candidate has given or confirmed; never invent employers, titles, dates, skills or numbers, and mark anything that needs a number as [X] with a question; quote the posting when you rely on it; and keep a running list of open questions for the candidate.

## Steps

Work through these steps in order. Do not skip a gate.

1. analyze (discover)
2. resume (build)
3. letter (build)
4. prep (learn)

### Step 1: Analyze the posting

Decode the posting before writing anything.

1. Summarise the role in one paragraph: the problem the hire solves, the real seniority judged by scope, and location or work-mode constraints.
2. Classify requirements as must-have, nice-to-have or boilerplate, quoting the posting, and infer hidden requirements from the responsibilities (mark them as inferences).
3. List red flags as neutral questions to ask, and the keywords a recruiter search or applicant tracking system would match, in the posting's spelling.
4. If the resume was provided, map each must-have to evidence (strong, partial, none), name the gaps and how each could be bridged honestly, and recommend apply, apply with a tailored angle, or skip. If it was not provided, ask for it now.
5. Name the two or three messages the whole application should prove. Steps 2 to 4 build on them.

Write the analysis as Markdown with sections Role, Requirements, Hidden requirements, Red flags, Keywords, Fit, Application angle.

Stop and wait for approval, and for the resume if it is missing.

Save this step's result to `applications/$slug/01-analysis.md`.

**Gate:** stop here and wait for the user's approval before step 2 (resume).

### Step 2: Tailor the resume

Tailor the resume to the approved application angle. Do not write a new resume from scratch.

1. Reorder and select: move the most relevant roles, projects and bullets up; cut or shorten what does not support the angle; keep chronology and dates truthful.
2. Rewrite the summary in three lines aimed at this role, and rewrite the most relevant bullets as action, scope and result. Use the posting's terms where they honestly describe the candidate's work.
3. Check keyword coverage: for each keyword from step 1, show whether it now appears, appears weakly, or is missing because the candidate lacks it. Never add a skill without evidence; list such gaps as questions instead.
4. Check format for applicant tracking systems: standard section headings, plain text dates, no text in images, tables, headers or footers, and both forms of key acronyms where useful.

Write the tailored resume in full, followed by a change log (what moved, what was cut, what was reworded and why), the keyword coverage table, and the [X] questions.

Stop and wait for approval.

Save this step's result to `applications/$slug/02-resume.md`.

**Gate:** stop here and wait for the user's approval before step 3 (letter).

### Step 3: Cover letter

Write a cover letter under 350 words that builds on the approved analysis and resume, in a direct tone unless the candidate asks otherwise.

1. Open with the strongest match to the role's main problem or a specific, true reason for wanting this job. Never open with "I am writing to apply".
2. For each of the two or three application messages, give one achievement as evidence and connect it to what the team needs. Select and connect; do not repeat the resume.
3. If there is an obvious question (career change, gap, relocation), answer it in one confident sentence.
4. Close with what the candidate would focus on first and a plain request to talk.

If the posting says no cover letter is wanted, write instead a 3-4 sentence note for the application form or for the recruiter, and say why.

Write the letter, then a list of [placeholders] and claims to check before sending.

Stop and wait for approval.

Save this step's result to `applications/$slug/03-cover-letter.md`.

**Gate:** stop here and wait for the user's approval before step 4 (prep).

### Step 4: Interview prep

Prepare the candidate for this role's interviews using the approved analysis, resume and letter.

1. Predict the questions: 5-8 behavioural or situational questions tied to the must-haves, 2-3 role-specific or technical topics to review, and the questions about the candidate's gaps or transitions that an interviewer is likely to probe.
2. Build 5-6 STAR stories from the candidate's experience (situation, task, action, result), each mapped to the questions it answers, with "I" actions and a result that is measured or clearly described. Mark any story that needs details the candidate must supply.
3. Write a 60-90 second "tell me about yourself" answer that leads to this role.
4. Write 6-8 questions for the interviewers, grouped by who to ask (recruiter, hiring manager, team members), that test the red flags from step 1.
5. List what to research about the company before the first interview, without stating facts you have not been given.

Write the prep pack as Markdown with sections Likely questions, Story bank, Tell me about yourself, Questions to ask, Research to do. End with a short checklist for the day before the interview.

Save this step's result to `applications/$slug/04-interview-prep.md`.
