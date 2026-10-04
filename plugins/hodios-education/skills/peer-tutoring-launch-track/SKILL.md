---
name: peer-tutoring-launch-track
description: Launches a school or university peer tutoring programme in gated steps, from goals and safeguarding to tutor training, matching, first sessions and an impact review after a term.
license: CC0-1.0
arguments:
  - setting
  - subjects
  - tutors
argument-hint: "[setting] <subjects> [tutors]"
disable-model-invocation: true
metadata:
  version: 1.1.0
  kind: workflow
  category: course-design
  source: https://hermes-ide.com/prompts/peer-tutoring-launch-track
  catalog: 2026.1004.0
---

# Peer tutoring launch track

## Inputs

- `setting` (optional; one of: primary, secondary, university; default: secondary): Where the programme runs. Sets the safeguarding approach, who can tutor whom, and how sessions are timetabled.
- `subjects` (required): The subjects or skills to be tutored and who needs help, e.g. "Year 7 reading fluency, tutored by Year 10" or "first-year statistics, tutored by second- and third-years".
- `tutors` (optional; default: 10): How many tutors you expect to recruit in the first term.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Launches a peer tutoring programme in a `$setting` setting, one approved step at a time: clear goals and a simple model, safeguarding and approvals, recruiting and training about $tutors tutors, matching tutors to tutees, running and supporting the first sessions, and reviewing impact after a term. Subjects and need:

<subjects>
$subjects
</subjects>

Peer tutoring works when it is structured: trained tutors, a set session routine, regular sessions over weeks, the right materials and staff monitoring. It does not work as unsupervised "homework buddies".

Each step produces one document and stops for the lead's approval; later steps build on approved decisions. Never invent policies, legal requirements or data; use placeholders such as [check with your safeguarding lead]. Refer to learners by role or code, never by name.

## Steps

Work through these steps in order. Do not skip a gate.

1. goals-and-design (plan)
2. safeguarding-and-approvals (plan)
3. recruit-and-train (build)
4. matching (build)
5. first-sessions (operate)
6. impact-review (review)

### Step 1: Goals and design

1. Ask in one message for anything missing: who the tutees are and how they are chosen, evidence of need, available time and space, and staff time for coordination.
2. Turn the subjects into two or three measurable first-term goals for tutees and tutors (for example fluency, quiz scores, confidence, attendance).
3. Recommend a model for a `$setting` setting with reasons: cross-age or same-age, one-to-one or small group, when sessions happen, and frequency (as a starting point, two or three 20-30 minute sessions a week for eight to ten weeks).
4. Draft the routine tutors follow every session, suited to the subject, and the materials needed.
5. Name the roles: coordinator, safeguarding contact, weekly tutor support.

Output: goals table (Goal | Measure | Baseline source | Target), model, routine, roles.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 2 (safeguarding-and-approvals).

### Step 2: Safeguarding and approvals

1. List the safeguarding measures for a `$setting` setting: sessions in visible, supervised spaces; no private contact or personal messaging outside sessions; a disclosure procedure (listen, never promise secrecy, tell the named staff contact the same day); how either side can ask to change partner or stop; background checks for adults working with under-18s [check with your safeguarding lead and local law]; data protection for progress data.
2. List approvals and communications: leadership, safeguarding lead, timetabling, family information or consent, staff briefing, each marked [check local policy].
3. Draft a one-page tutor code of conduct and a plain-language note for tutees and families.
4. Write a risk register (Risk | Likelihood | Impact | Control | Owner) covering safeguarding, tutor workload, tutee stigma, missed sessions and inaccurate teaching.

Output: safeguarding measures, approvals checklist, code of conduct, family note, risk register.

Stop for approval. No recruiting yet.

**Gate:** stop here and wait for the user's approval before step 3 (recruit-and-train).

### Step 3: Recruit and train

1. Draft a recruitment message for about $tutors tutors: the role, time commitment, what they gain, how to apply. Select for reliability, patience and secure knowledge, not only top grades.
2. Plan short training sessions: the routine, explaining without giving answers (wait, prompt, hint, model), specific praise, the materials, session logs, the code of conduct and disclosure steps, and what to do when they do not know the answer (say so, check together, flag it in the log), and role-plays (a silent tutee, one who wants answers, one who is upset).
3. Add a readiness check: an observed practice session with a checklist.
4. Plan ongoing support: regular tutor huddles, help between sessions, end-of-term recognition.

Output: recruitment message, training plan with timings, readiness checklist, support plan.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 4 (matching).

### Step 4: Matching

1. Ask for anonymised tutor and tutee details (codes, strengths and needs, availability, relevant considerations) if not given.
2. Propose matching rules: tutor secure in what the tutee needs, a suitable age or attainment gap, shared availability, no known conflicts. Staff judgement overrides the rules.
3. Draft a matching table (Tutor code | Tutee code | Reason | Watch?).
4. Set the baseline: the Step 1 measures taken before the first session, and a comparison group if feasible, with its limits stated.
5. Draft a session log: date, what was covered, how it went, any concern.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 5 (first-sessions).

### Step 5: First sessions

1. Plan each pair's first session: introductions, the tutee's goal in their own words, an easy early win using the routine.
2. Set monitoring: coordinator drop-ins in the first fortnight with an observation checklist (routine followed, tutee doing the thinking, tone, materials pitched right) and weekly log reading.
3. Prepare responses to common problems: missed sessions, a tutor giving answers, a disengaged tutee, a poor match, wrong-level materials, and any safeguarding concern (Step 2 procedure, same day).
4. In week two, check privately with tutors and tutees how it is going and whether supervision works in practice.
5. Provide a two-week check-in template: attendance, observations, issues, actions.

Output: first-session plan, observation checklist, problem responses, check-in template.

Ask the lead to share how the first weeks went, adjust, and stop until the term is complete.

**Gate:** stop here and wait for the user's approval before step 6 (impact-review).

### Step 6: Impact review

1. Ask for end-of-term data: the baseline measures again, attendance, a summary of session logs, and feedback from tutors, tutees, families and staff.
2. For each goal give baseline, end point and change, and how many tutees improved, stayed level or fell back. Compare with any comparison group and state plainly what the data cannot show (small numbers, no random assignment, other support).
3. Review implementation: frequency achieved, routine fidelity, which pairs worked and why. Include benefits for tutors and whether the load on them was fair, especially near their own exams.
4. Recommend what to keep, change or stop, and whether to scale.
5. Draft a one-page leadership summary and a short celebration note for tutors and families, with no learner identifiable.

Output: results table (Goal | Baseline | End | Change | Notes), findings, recommendations, both drafts.
