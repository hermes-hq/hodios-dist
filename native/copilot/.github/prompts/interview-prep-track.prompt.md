---
description: Prepares for one specific interview in gated steps - decode the role, build a story bank, run a scored mock, prepare questions to ask and plan the day. Use once an interview is booked.
agent: agent
argument-hint: job_posting background interview_date slug
---

# Interview prep track

Prepares the candidate for one booked interview the way a good interview coach would over a few sessions: work out what this interview will actually test, build true stories that prove it, rehearse under realistic pressure, prepare questions that show judgement, and plan the day so nothing practical gets in the way. Each step writes one artifact and stops for approval; later steps reuse the approved artifacts instead of asking again.

<job_posting>
${input:job_posting:The job posting, plus what you know about the interview - stage, format (video, in person, panel), length, who you will meet, any task or presentation.}
</job_posting>

<background>
${input:background:Your resume and notes on your experience, achievements and why you want this role.}
</background>
Only if interview_date was provided (leave it empty to skip): 
Interview date: ${input:interview_date:Optional. When the interview is, so the plan fits the time left.}

Rules for every step: use only facts the candidate has given or confirmed; never invent employers, results, numbers or company facts, and mark gaps as [X] with a question; quote the posting when you rely on it; label anything about the employer's process that was not given as an assumption; and keep a running list of open questions for the candidate. If the time before the interview is short (under two days), say so and offer a compressed path: decode and stories together, a five-question mock, then the day plan.

## Steps

Work through these steps in order. Do not skip a gate.

1. decode (discover)
2. stories (build)
3. mock (verify)
4. questions (build)
5. day (ship)

### Step 1: Decode the role and the interview

Work out what this interview will test before preparing any answers.

1. In one paragraph: the problem this hire solves, the real seniority judged by scope, and what the interview stage and format given suggest about who is assessing what (recruiter, hiring manager, peers, panel, task).
2. List the four to six competencies or criteria the interviewers are most likely to score, each with the line of the posting it comes from. Separate must-haves from nice-to-haves.
3. Predict the questions: six to ten behavioural or situational questions tied to those competencies, two or three role-specific or technical topics to refresh, and the awkward questions this background invites (a gap, a short tenure, a missing must-have, a career change, a layoff).
4. Map each competency to the candidate's evidence (strong, partial, none) and name the two or three messages the candidate should leave the interviewers with.
5. Say what to research about the company and team before the interview, without stating facts that were not given.

Write the artifact as Markdown with sections Role, What will be scored, Likely questions, Evidence map, Key messages, Research to do.

Stop and wait for approval. Ask the candidate to correct anything about the format or interviewers that you assumed.

Save this step's result to `interviews/${input:slug:Short kebab-case name for this interview, used for the folder the step artifacts are saved in (for example acme-pm-final).}/01-role-decoded.md`.

**Gate:** stop here and wait for the user's approval before step 2 (stories).

### Step 2: Build the story bank

Turn the candidate's real experience into stories that cover the approved competencies.

1. Draft six to eight stories in STAR form (situation, task, action, result). Keep the situation and task to two sentences; put most of the words into what the candidate personally did, in "I" form; end with a measured or clearly described result and one line on what they learned.
2. Make each story flexible: note which competencies and predicted questions from step 1 it can answer, and how to angle it for each.
3. Cover every must-have with at least one story, and include at least one story about a failure or a mistake and one about a disagreement or conflict, since most interviews ask for both.
4. Write a 60 to 90 second answer to "Tell me about yourself" in present-past-future order that leads to this role, and short, truthful answers to each awkward question from step 1.
5. List the details the candidate must supply for any story marked with [X], as specific questions.

Write the artifact as Markdown with sections Story bank (one subsection per story with STAR, competencies, angles), Coverage table (Competency | Stories), Tell me about yourself, Awkward questions, Details needed.

Stop and wait for approval and for the missing details. Do not start the mock until the candidate confirms the stories are accurate.

Save this step's result to `interviews/${input:slug:Short kebab-case name for this interview, used for the folder the step artifacts are saved in (for example acme-pm-final).}/02-story-bank.md`.

**Gate:** stop here and wait for the user's approval before step 3 (mock).

### Step 3: Run a mock interview

Rehearse under realistic conditions, then give honest, specific feedback.

1. Explain in one line: about six questions in the style of this stage, one at a time, with probes, feedback at the end (or after each answer if the candidate prefers).
2. Ask one question at a time from the predicted list, covering the key competencies and at least one awkward question. Wait for each answer. Probe where a real interviewer would (vague result, "we" instead of "I", a skipped part). Stay neutral; no coaching mid-answer.
3. Then score each answer 1 to 4 against its competency (1 no evidence, 2 vague, 3 clear, 4 strong with a measured result and reflection), with one sentence on why.
4. For the two weakest answers, show a stronger version using only the candidate's real material, and name one delivery habit to fix (length, filler, burying the result, not answering the question).

Write the artifact as Markdown with sections Questions asked, Scores (table: Question | Competency | Score | Why), Stronger versions, Habits to fix.

Stop and wait for approval. Offer a second round on the weakest competencies.

Save this step's result to `interviews/${input:slug:Short kebab-case name for this interview, used for the folder the step artifacts are saved in (for example acme-pm-final).}/03-mock-feedback.md`.

**Gate:** stop here and wait for the user's approval before step 4 (questions).

### Step 4: Prepare questions to ask

1. Write six to eight questions grouped by who the candidate will meet (recruiter, hiring manager, peers, senior leader): what success looks like in six months, the team's biggest problem, how decisions and performance are judged, why the role is open, next steps.
2. Add one or two neutral questions that test any concern from step 1 (a vague responsibility, turnover, an unclear reporting line).
3. For each, note what a good and a worrying answer sound like.
4. Mark the two to ask if time is short, and a closing question on next steps and timeline. Leave out anything on the company website or premature at this stage.

Write the artifact as Markdown with sections Questions by interviewer, Concerns to test, What to listen for, If time is short.

Stop and wait for approval.

Save this step's result to `interviews/${input:slug:Short kebab-case name for this interview, used for the folder the step artifacts are saved in (for example acme-pm-final).}/04-questions-to-ask.md`.

**Gate:** stop here and wait for the user's approval before step 5 (day).

### Step 5: Plan the day

1. A countdown to the interview (use the date if given): final run-through of the stories, research to finish, and no new stories the night before.
2. Logistics for the format: video (platform, camera, sound, light, backup number), in person (route, arrival, who to ask for, what to bring), panel or task (timing, materials).
3. A one-page brief for the last 30 minutes: three key messages, one line per story with its competency, the opening answer in three beats, the two must-ask questions, and salary range, notice period and start date if given.
4. Recovery lines for blanking, misunderstanding a question or a weak answer, and how to ask for a moment to think.
5. After: note the questions within the hour, send a specific thank-you within 24 hours, and record what to improve.

Write the artifact as Markdown with sections Countdown, Logistics, One-page brief, Recovery lines, After the interview. End with any unresolved open questions.

Save this step's result to `interviews/${input:slug:Short kebab-case name for this interview, used for the folder the step artifacts are saved in (for example acme-pm-final).}/05-day-plan.md`.
