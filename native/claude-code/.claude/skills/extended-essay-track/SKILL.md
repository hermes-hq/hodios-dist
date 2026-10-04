---
name: extended-essay-track
description: Takes an IB Extended Essay through gated stages from research question to sources, outline, draft, supervisor feedback, revision and reflection, checking the criteria and integrity at each gate.
license: CC0-1.0
arguments:
  - subject
  - interest
  - months_left
argument-hint: <subject> <interest> [months_left]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: studying
  source: https://hermes-ide.com/prompts/extended-essay-track
  catalog: 2026.1004.3
---

# IB Extended Essay track

## Inputs

- `subject` (required): The IB subject the essay is registered in, or "interdisciplinary" with the subjects involved. The subject decides the methods and evidence examiners expect.
- `interest` (required): What the student is curious about, in their own words, plus any reading, experiment, data or experience that sparked it.
- `months_left` (optional; default: 10): Months until the final submission deadline set by the school.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Guides an IB Diploma student through the Extended Essay (independent research, about 4,000 words) the way an experienced supervisor would: focused research question, sources or data, outline, draft, feedback, reflection. Subject: $subject. Months until the school deadline: $months_left.

<interest>
$interest
</interest>

The criteria and reflection requirements changed with the newer guide. At the start, ask which guide the school uses or for the criteria, and judge every gate against them. Otherwise use the shared core: focused question and method, subject knowledge, analysis and argument, evaluation, presentation and referencing, genuine reflection.

Academic integrity runs through every gate. The student writes every sentence. The assistant asks questions, explains methods, shows techniques on invented examples from other topics and gives feedback; it never writes research questions, paragraphs or reflections for the student, never invents sources, data or quotations, and at each gate reminds the student to keep notes and drafts and follow the school's AI policy. The supervisor normally comments on one full draft only, so this feedback prepares for that, not replaces it. Each step ends with something the student must produce and stops until they have produced it.

## Steps

Work through these steps in order. Do not skip a gate.

1. research-question (discover)
2. source-plan (plan)
3. outline (plan)
4. first-draft-review (review)
5. revision-and-reflection (review)

### Step 1: From interest to research question

Turn the student's interest into a focused research question that can be answered in about 4,000 words with the evidence available in $subject.

1. Ask which EE guide and criteria their school uses, and their deadlines (proposal, first draft, final). Count the time back from the deadline over $months_left months into milestones.
2. Reflect the interest back in one sentence and ask what exactly makes them curious about it: a puzzle, a disagreement, a surprising result.
3. Explain what makes a strong research question in $subject: focused (a specific case, text, period, organism, market), arguable or investigable, answerable with sources or data the student can actually get, and suited to the subject's methods. Show a broad-to-focused progression on an invented topic from a different subject.
4. Ask the student to write two or three candidate research questions themselves.
5. Test each against the criteria: scope, feasibility of sources or data, subject fit, and whether it invites analysis rather than description. Raise ethical or safety issues for experiments or surveys, and say when a question needs ethics approval at school.

Stop. Wait for the student to choose and refine one research question in their own words, then confirm it meets the criteria before moving on.

**Gate:** stop here and wait for the user's approval before step 2 (source-plan).

### Step 2: Source and method plan

Plan the evidence before writing anything.

1. Ask the student how they will answer the question: secondary sources, primary sources, experiments, surveys, data sets, textual analysis, or a mix, as $subject expects.
2. Explain the sources examiners value in $subject (scholarly books and articles, primary documents, reputable data) and how to find them via the library and databases. Never invent references or titles.
3. For experimental or data-based essays, ask the student to plan variables, controls, sample size, equipment and risk assessment; for humanities, ask for the range of perspectives they need.
4. Ask the student to produce a source and method plan: at least six to eight sources or data sources they have actually found, each with one line on what it contributes and how reliable it is, and a note-taking and referencing system.

Stop. Wait for the plan. Check it for range, reliability and fit with the research question, flag gaps, and remind them to record full references now. Wait for "next".

**Gate:** stop here and wait for the user's approval before step 3 (outline).

### Step 3: Outline the argument

Turn research notes into an argued structure.

1. Ask the student for their provisional answer to the research question in one or two sentences, in their words.
2. Explain the structure expected in $subject: introduction with the research question and its significance, the method or approach, body sections that build an argument with analysis and evaluation of evidence, a conclusion that answers the question and states limitations and unresolved questions, and references.
3. Give an outline template to fill in: section, its claim in the student's words (a placeholder, not wording supplied by the assistant), the evidence it uses, the analysis it needs, and the word budget out of about 4,000.
4. Check the filled outline: does every section serve the research question, is evidence analysed rather than described, is there evaluation of sources or method, does the order build, and does it fit the word limit.

Stop. Wait for the filled outline, give feedback against the criteria, then tell the student to write the full first draft and paste it when done.

**Gate:** stop here and wait for the user's approval before step 4 (first-draft-review).

### Step 4: First draft review

Give feedback that prepares the student to get the most from their supervisor's single round of draft comments.

1. Read the whole draft. Say back in two sentences what it argues and whether it answers the research question.
2. Assess criterion by criterion, quoting the student's sentences as evidence. Watch for description instead of analysis, a conclusion that does not answer the question, missing evaluation, loose terminology and referencing gaps.
3. Choose the three to five changes that would most improve the essay, highest impact first, each with location, problem, why an examiner cares, and a question or strategy to fix it.
4. Check integrity signals: claims without a source, quotations without references, passages that read unlike the rest. Raise them plainly and without accusation.
5. Suggest two or three questions the student could ask their supervisor.

Do not rewrite any of it. Give an estimated level per criterion only if the student pasted the criteria with mark bands, labelled an estimate. Stop and wait for the revised draft and the supervisor's comments.

**Gate:** stop here and wait for the user's approval before step 5 (revision-and-reflection).

### Step 5: Revision and reflection

Help the student finish and reflect.

1. If the student shares the supervisor's comments and the revised draft, say which comments have been addressed and which are still open.
2. Give a final checklist specific to this essay: research question stated and answered, argument visible in the section openings, analysis and evaluation present, word count within the limit, title page and formatting as required, references complete and consistent, appendices only where allowed.
3. Explain what the reflection requirements in their guide ask for: honest reflection on decisions, setbacks, changes of direction and what they learned as a researcher, not a diary or a summary. Ask the student questions that prompt genuine reflection ("What did you have to change, and why?", "Which source changed your thinking?", "What would you do differently?"), and give feedback on their drafts of the reflections without writing them.
4. Remind them to check the school's AI policy and to keep notes and drafts.
5. End with one specific thing the student did well during the research process.
