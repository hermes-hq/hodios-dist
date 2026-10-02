---
name: course-design-track
description: Takes a course from audience and outcomes to an outline, assessments, lesson materials and a review pass, pausing for approval between steps. Use when building a whole course.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: course-design
  source: https://hermes-ide.com/prompts/course-design-track
  catalog: 2026.1002.2
---

# Course design track

## Inputs

- [COURSE_NAME] (required): Working title of the course, used to label every step's output.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Designs the course "[COURSE_NAME]" by backward design, one approved step at a time: who it is for and what they will be able to do, then the module outline, then the assessments that prove the outcomes, then the materials for each session, then an alignment and quality review. Each step produces one document and stops for the designer's approval or edits; later steps build on the approved versions instead of re-asking. The designer stays in charge of every decision about scope, content and standards; the assistant drafts, checks alignment and flags gaps.

## Steps

Work through these steps in order. Do not skip a gate.

1. audience-outcomes (discover)
2. outline (design)
3. assessments (design)
4. materials (build)
5. review (review)

### Step 1: Audience and outcomes

Establish who "[COURSE_NAME]" is for and what they will be able to do at the end.

1. Ask the designer, in one message, for anything not already given: the learners (background, prior knowledge, motivation), the setting (school, university, workplace, online), the length and session pattern, any required standards or syllabus, constraints (class size, technology, budget), and how the course will be judged a success.
2. When you have the answers, write:
   - **Learner profile:** 4 to 6 bullets, including likely misconceptions and barriers.
   - **Course outcomes:** 4 to 6 outcomes, each one sentence with one observable verb (no "understand" or "know"), at levels that fit the audience and the time, most at apply or above.
   - **Out of scope:** what the course deliberately does not cover.
   - **Assumptions:** anything you assumed rather than were told.
3. Flag any outcome that is unrealistic for the time available.

Stop and wait for approval or edits. Do not start the outline.

**Gate:** stop here and wait for the user's approval before step 2 (outline).

### Step 2: Outline

Using the approved outcomes for "[COURSE_NAME]", build the module outline.

1. List the concepts and skills each outcome depends on, and order them by prerequisite.
2. Group them into modules or weeks that fit the approved length and session pattern. Front-load foundations, revisit key ideas later in new contexts, and leave a consolidation point about two-thirds through plus time for the final assessment.
3. Produce a table: Module | Title | Outcomes served | Key concepts | Session time | Independent time.
4. Check that every outcome is served by at least one module and that every module serves at least one outcome. Remove or merge modules that serve none.
5. State the weekly learner workload and flag any week that is heavier than the rest.

Stop and wait for approval or edits. Do not design assessments yet.

**Gate:** stop here and wait for the user's approval before step 3 (assessments).

### Step 3: Assessments

Design the evidence that learners in "[COURSE_NAME]" have met the approved outcomes.

1. **Summative:** one or two assessments in which learners perform the outcomes, preferably an authentic task (a project, case analysis, portfolio, performance or practical). For each: the brief as learners will read it, the outcomes it assesses, its weight, and when it is due in the outline.
2. **Rubric:** an analytic rubric for each summative task, with 3 to 6 non-overlapping criteria and 4 levels whose descriptors name observable features of the work, not adjectives.
3. **Formative:** one low-stakes check per module (a quiz, an exit ticket, a draft with peer feedback, a short practical), with what the teacher does with the results.
4. **Alignment matrix:** outcomes as rows, assessments as columns. Every outcome is assessed summatively at least once; flag any that are not.

Stop and wait for approval or edits. Do not write session materials yet.

**Gate:** stop here and wait for the user's approval before step 4 (materials).

### Step 4: Materials

Write the materials for "[COURSE_NAME]" one module at a time. Ask which module to start with if the designer has not said; default to module 1.

For each module:
1. **Session plan:** objectives for the session, a timed sequence (opener, explicit teaching with a worked example, guided practice, independent or group practice, check for understanding, close) with timings that add up to the session length.
2. **Content notes:** the explanations, examples and key questions the teacher needs, written out, not summarised.
3. **Learner materials:** worksheets, readings described by type and level, task cards or slides outlines, as text the designer can paste.
4. **The formative check** from Step 3, written in full with answers.
5. **Differentiation:** support and stretch options for this module.

Do not invent specific book titles, authors or URLs; describe the resource needed instead.

After each module, stop and wait for approval before writing the next. When the designer says the materials are done, move on to the review.

**Gate:** stop here and wait for the user's approval before step 5 (review).

### Step 5: Review

Review the whole of "[COURSE_NAME]" as an independent course reviewer would, using the approved outcomes, outline, assessments and materials.

Check and report:
1. **Alignment:** every outcome is taught, practised and assessed; every activity and assessment serves an outcome. List any break in the chain.
2. **Load and pacing:** weekly workload is realistic and even; no module crams new ideas without practice.
3. **Assessment quality:** briefs are clear, rubrics are observable and non-overlapping, and summative tasks actually require the outcome's verb.
4. **Accessibility and inclusion:** materials are readable, alternatives exist for any inaccessible format, examples are varied and free of stereotypes.
5. **Accuracy:** statements that should be checked by a subject expert, listed rather than asserted.

Output a table: Area | Finding | Severity (must fix / should fix / consider) | Suggested fix. Rank must-fix items first, then end with the three changes that would most improve the course. Make no edits yourself; the designer decides what to change.
