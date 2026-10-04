---
name: lesson-materials-track
description: Takes one lesson from plan to slide outline, worksheet, quiz and differentiated versions, pausing for teacher approval after each step. Use to prepare a complete, consistent lesson pack.
license: CC0-1.0
arguments:
  - topic
  - grade_level
  - minutes
argument-hint: <topic> <grade_level> [minutes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: teaching
  source: https://hermes-ide.com/prompts/lesson-materials-track
  catalog: 2026.1004.0
---

# Lesson materials track

## Inputs

- `topic` (required): What the lesson teaches, plus any standard or curriculum point it must meet, e.g. "photosynthesis - inputs, outputs and where it happens".
- `grade_level` (required): Grade, year or course, e.g. "Grade 7 science", "Year 4", "adult ESL intermediate".
- `minutes` (optional; default: 50): Lesson length in minutes.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Builds a complete, consistent pack for one $minutes-minute lesson on **$topic** for **$grade_level**: the lesson plan, a slide outline, a student worksheet, a short quiz, and support and stretch versions of the worksheet and quiz. Each step produces one document and stops for the teacher's approval or edits; later steps use the approved versions exactly (same objectives, vocabulary, examples and numbers) instead of re-asking or drifting. If the teacher asks to skip the approvals, say in one sentence that each step builds on the approved one before it, and continue only once they confirm; even then, produce the steps in order under their own headings. The teacher decides what is taught and how; the assistant drafts, keeps the materials aligned and checks every answer. Nothing is invented about the school's curriculum, resources or technology beyond what the teacher supplies; assumptions are stated, not hidden.

## Steps

Work through these steps in order. Do not skip a gate.

1. lesson-plan (plan)
2. slide-outline (build)
3. worksheet (build)
4. quiz (verify)
5. differentiated-versions (build)

### Step 1: Lesson plan

Write the plan the rest of the pack will follow.

1. If anything essential is missing (what students learned before, available technology, class size, any students with specific needs), ask for it in one short message. If the teacher prefers not to answer, state reasonable assumptions and continue.
2. Write 1 to 3 measurable objectives (observable verbs, no "understand") and matching student-facing success criteria ("I can…").
3. List the key vocabulary (5 to 8 terms with student-friendly definitions) and the 2 or 3 misconceptions students are likely to bring.
4. Sequence the lesson with timings that add up exactly to $minutes minutes: retrieval opener, explicit teaching with one fully written worked example or model, guided practice, independent practice (this is where the worksheet will be used), a short quiz or exit check, and closure. Keep any single block of teacher talk to about 10 to 15 minutes.
5. Mark the two points where the teacher checks understanding and what they do if many students are wrong.
6. Add a materials list that names the slide deck, worksheet and quiz the next steps will produce.

Stop and wait for approval or edits. Do not start the slides.

**Gate:** stop here and wait for the user's approval before step 2 (slide-outline).

### Step 2: Slide outline

Turn the approved lesson plan into a slide outline the teacher can build quickly in any presentation tool.

1. One entry per slide, in lesson order, with: slide number, the lesson phase it belongs to, the title, the on-slide content and speaker notes for the teacher.
2. Keep on-slide text minimal: a question, a diagram description, a worked example step, or at most three short lines. Put explanations in the speaker notes, not on the slide.
3. Include the retrieval opener questions (with answers in the notes), the worked example split across slides so steps can be revealed one at a time, the check-for-understanding questions from the plan, and the success criteria at the start and end.
4. For every image or diagram, describe what it should show and suggest a simple way to make it (a labelled sketch, a table); never claim a specific image or source exists. Add alt text for each.
5. Use the plan's vocabulary, examples and numbers exactly. Aim for roughly one slide per 2 to 4 minutes of lesson time.

Stop and wait for approval or edits. Do not write the worksheet yet.

**Gate:** stop here and wait for the user's approval before step 3 (worksheet).

### Step 3: Worksheet

Write the student worksheet for the guided and independent practice in the approved plan.

1. Start with the lesson title, the "I can" statements and a short reminder box (the key vocabulary or the worked-example method from the slides).
2. Section A, guided practice: 2 to 4 tasks done with the teacher, mirroring the worked example.
3. Section B, independent practice: 4 to 8 tasks of rising difficulty that match the objectives, with at least one that applies the idea in a new context and one that targets a misconception from the plan.
4. Section C, challenge: 1 or 2 deeper tasks for students who finish early (reasoning, explaining, creating), not just more of the same.
5. Size the worksheet to the independent-practice time in the plan; say how long each section should take.
6. Write instructions at the class's reading level, with clear space to answer.
7. Provide an answer key with worked solutions or model answers, checked for correctness, separately from the student version.

Stop and wait for approval or edits. Do not write the quiz yet.

**Gate:** stop here and wait for the user's approval before step 4 (quiz).

### Step 4: Quiz

Write a short quiz that checks the approved objectives at the end of the lesson or at the start of the next one.

1. 5 to 8 questions, answerable in the time the plan allows (typically 5 to 10 minutes). Cover every objective; include at least one question that would expose each listed misconception.
2. Use a mix that fits the age and topic: multiple choice with plausible distractors drawn from misconceptions (one correct answer, no "all of the above", options of similar length), short answer, and one question that asks students to explain or apply.
3. Do not reuse worksheet questions word for word; test the same skills in a slightly different way.
4. Provide an answer key and, for each multiple-choice distractor, the misconception it reveals, so the teacher can act on the results.
5. Add a one-line guide: what score or pattern means re-teach, and what to re-teach.

Stop and wait for approval or edits. Do not write the differentiated versions yet.

**Gate:** stop here and wait for the user's approval before step 5 (differentiated-versions).

### Step 5: Differentiated versions

Adapt the approved worksheet and quiz so every student works toward the same objectives.

1. **Support version** of the worksheet and quiz: same objectives and the same core tasks, with scaffolds instead of easier content: a partly completed worked example, sentence starters, a word bank with the lesson vocabulary, chunked multi-step tasks, fewer but representative questions, simpler language and clearer layout.
2. **Stretch version** of the worksheet: the same core tasks with more open demands: explain why, generalise, find the error, create an example, connect to another topic. Not simply more questions.
3. **Multilingual learners:** key vocabulary with visuals or simple definitions, sentence frames for explanations, and a note on any idioms or culturally specific contexts to change.
4. Keep the quiz answers comparable across versions so results can be read together; say which questions are shared.
5. Finish with a pack summary: a list of every file in the pack (plan, slides, worksheet, quiz, support and stretch versions, answer keys) and a final consistency check confirming that objectives, vocabulary, examples and answers match across all materials, noting anything the teacher should adjust.
