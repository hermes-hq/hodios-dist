---
name: exam-prep-track
description: Takes a learner from a syllabus to a diagnostic quiz, a weighted study plan, targeted practice and a final mock with review, pausing between steps. For students preparing for a specific exam.
license: CC0-1.0
arguments:
  - exam
  - syllabus
  - exam_date
  - hours_per_week
argument-hint: <exam> <syllabus> <exam_date> [hours_per_week]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: workflow
  category: exam-prep
  source: https://hermes-ide.com/prompts/exam-prep-track
  catalog: 2026.1004.3
---

# Exam preparation track

## Inputs

- `exam` (required): The exam, as precisely as possible, e.g. "AQA GCSE Chemistry Paper 1 (Higher)", "MCAT Chem/Phys section", "first-year Linear Algebra final".
- `syllabus` (required): The syllabus, specification or topic list, pasted, plus anything known about the exam format (question types, length, marks, allowed materials).
- `exam_date` (required): The exam date. Include today's date too if the assistant may not know it, so the weeks can be counted.
- `hours_per_week` (optional): Realistic study hours per week for this exam, after other commitments. Asked for in step 2 if missing.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Prepares the learner for $exam on $exam_date the way a good tutor would: find out what they already know before planning anything, spend the hours where the marks are, practise by retrieval rather than rereading, and prove readiness with a timed mock under exam conditions. Each step ends with something the learner has to do (sit the diagnostic, approve the plan, finish practice, sit the mock) and stops until they have done it. Later steps use the results of earlier ones instead of re-asking. Throughout, the assistant writes questions in the exam's own style, marks honestly, never invents facts about the exam's format or grade boundaries, and asks when the syllabus leaves something unclear.

## Steps

Work through these steps in order. Do not skip a gate.

1. diagnose (discover)
2. plan (plan)
3. practice (learn)
4. mock (verify)
5. review (review)

### Step 1: Map the syllabus and diagnose

Turn the syllabus for $exam into a topic map, then find out what the learner already knows.

<syllabus>
$syllabus
</syllabus>

1. Build the topic map: group the syllabus into 6 to 15 topics. For each, give its weight in the exam (from the syllabus or format if stated; otherwise estimate from the share of content and label it "estimated") and the question types it appears in.
2. If the exam format is not clear from what was given (question types, number of papers, timing, allowed calculator or formula sheet), list what is missing and ask. Do not invent the format or any grade boundaries.
3. Write a diagnostic quiz the learner can finish in 30 to 45 minutes. Budget the time first, from the question types (roughly 1 minute per multiple-choice item, 3 to 5 per short answer, 8 to 12 per multi-step problem), then spread the questions:
   - 1 to 3 questions per topic, weighted toward heavily weighted topics, written in the exam's own style and command words. With many topics, give light topics one question each rather than overrunning the time.
   - A mix of recall, application and one multi-step question for the biggest topics.
   - Numbered and labelled by topic, with marks per question.
   - No answers or hints in this message.
4. Tell the learner how to take it: closed book, timed, and to mark each answer with a confidence of 1 (guess) to 3 (sure), because a lucky guess and a secure answer need different plans.

Stop. Wait for the learner's answers before marking anything or planning.

**Gate:** stop here and wait for the user's approval before step 2 (plan).

### Step 2: Mark the diagnostic and build the weighted plan

Mark the learner's diagnostic answers and build a study plan from now until $exam_date.

1. Mark every answer against a correct solution you have worked out and checked. For each question give: right or wrong, the marks earned, and for wrong answers the specific error in one line. Be honest; do not round up.
2. Score each topic as a priority: combine the topic's exam weight with the learner's result and confidence. A heavily weighted topic answered wrongly or with low confidence comes first; a correct answer marked "guess" counts as not secure.
3. Work out the time available: the weeks until $exam_date and Only if hours_per_week was provided: $hours_per_week hours per week. If the hours per week were not given, or today's date is unknown, ask before planning. If the time is clearly too short to cover everything, say so and plan for the most marks per hour.
4. Build the plan:
   - Hours allocated per topic in proportion to priority, with every topic revisited at least twice on a spaced schedule (for example, after 2 days, then a week, then three weeks).
   - Weekly sessions, each with a specific goal stated as something the learner will be able to do, a retrieval activity (practice questions, flashcards, blank-page recall) and a self-test. No session that is only rereading or highlighting.
   - Mixed practice across topics in the later weeks, once each topic has been learned on its own.
   - About 15 percent slack for missed sessions, and the final week reserved for the mock and light review.
5. Present it as a table: Week | Topics | Session goals | Practice | Hours. Then list the top three priorities in a sentence each.

Stop. Ask the learner to approve or adjust the plan, then work through it and come back for practice.

**Gate:** stop here and wait for the user's approval before step 3 (practice).

### Step 3: Targeted practice

Run practice for $exam on the priority topics from the approved plan, one set at a time.

1. Ask which topic or session from the plan the learner is working on now, unless they say.
2. Give a practice set of 4 to 8 exam-style questions on that topic, ordered from straightforward to exam-hard, with the marks for each. Include at least one question that mixes in an earlier topic.
3. Wait for the answers. Then mark each one: what earned marks, what lost marks and why, and the one thing to do differently. When a mistake shows a misunderstanding, explain the idea briefly and give one new question that tests it, rather than only showing the correct answer.
4. Keep a running tracker across sets: Topic | Sets done | Latest score | Secure? (yes when the learner scores at least 80 percent on two sets in a row, on different days).
5. When a topic is secure, move to the next priority. When the learner reports a topic is going slower than planned, adjust the plan's remaining weeks and say what moves.

Repeat this step as many times as the learner wants. When every high-priority topic is secure, or the learner says they are ready, stop and suggest moving to the mock. Do not start the mock until they agree.

**Gate:** stop here and wait for the user's approval before step 4 (mock).

### Step 4: Final mock exam

Write a full mock of $exam that matches the real exam as closely as the information allows.

1. Match the format: same sections, question types, number of questions, total marks and time. If any of these are unknown, use your best reconstruction, label it, and keep it consistent with the syllabus.
2. Cover the syllabus in proportion to the topic weights, with no repeats of practice questions. Include the harder end of the exam: multi-step, unfamiliar context and extended-response questions where the exam has them.
3. Give clear instructions: total time, materials allowed, and the advice to sit it in one go under exam conditions, timed, closed book, and to note the time at the end of each section.
4. Do not include answers, hints or a mark scheme in this message.

Stop. Wait for the learner's completed answers and their section times.

**Gate:** stop here and wait for the user's approval before step 5 (review).

### Step 5: Mock review and final days

Mark the learner's mock of $exam and plan the days left until $exam_date.

1. Mark every question against a worked, checked solution. Give the total, the score per section and per topic, and compare with the diagnostic from step 1.
2. Classify each lost mark: knowledge gap, misread question, careless slip, time pressure or method error. Use the section times to spot time pressure.
3. Give a readiness verdict per topic: secure, nearly secure, or at risk. Base it on the mock and the practice tracker, and be candid. Do not predict a grade unless real grade boundaries were provided.
4. Plan the remaining days: short targeted review on at-risk topics, one mixed timed practice set, a checking routine against the slip types found, and nothing new in the final 24 hours. Include practical exam-day preparation: materials, timing per section, and what to do when stuck on a question.
5. End with three things the learner is doing well, named specifically.
