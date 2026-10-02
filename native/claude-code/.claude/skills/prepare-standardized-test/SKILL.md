---
name: prepare-standardized-test
description: Builds a strategy for one section of a standardised test such as the SAT, ACT, GRE, GMAT or LSAT, covering question types, timing, traps, a diagnostic and a drill plan. For students with a test date.
license: CC0-1.0
arguments:
  - test
  - section
  - current_score
  - target_score
  - test_date
argument-hint: <test> <section> [current_score] [target_score] [test_date]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: exam-prep
  source: https://hermes-ide.com/prompts/prepare-standardized-test
  catalog: 2026.1002.2
---

# Prepare for a standardised test section

## Inputs

- `test` (required): The test, e.g. "digital SAT", "ACT", "GRE General", "GMAT Focus", "LSAT", "IELTS Academic".
- `section` (required): The section to plan for, e.g. "Math", "Reading and Writing", "Quantitative Reasoning", "Logical Reasoning".
- `current_score` (optional): Optional current section score and where it came from (official practice test, diagnostic, previous sitting).
- `target_score` (optional): Optional target section score, ideally from the programmes being applied to.
- `test_date` (optional): Optional test date, plus today's date if the assistant may not know it.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Standardised tests reward a specific, learnable mix of content, question-type recognition and pacing, and most score gains come from fixing a few recurring error patterns rather than from studying everything. The formats also change: the SAT went digital and section-adaptive, the GRE and GMAT were shortened and restructured, the LSAT dropped Analytical Reasoning, and the ACT made Science optional. A plan built on an outdated format wastes weeks.
</context>

<task>
Build a preparation strategy for the $section section of the $test.
Only if current_score was provided: Current score: $current_score.
Only if target_score was provided: Target score: $target_score.
Only if test_date was provided: Test date: $test_date.

1. **Section at a glance.** State the current format as you understand it: number of questions, time, whether it is adaptive and how, calculator and other rules, and how the section is scored. Mark this "check against the official test-maker's site", and flag any part you are less sure of, especially if the format changed recently. If the test or section name does not match a format you know, say so and ask.
2. **Question types.** List the question types in this section with their approximate share, the skill each tests and a one-line approach for each. Do not quote exact counts unless you are confident they are official.
3. **Timing strategy.** Average time per question, checkpoint times, how adaptivity (if any) changes the value of early questions, when to guess and move on (only where there is no penalty for wrong answers; say if there is), and a flag-and-return routine.
4. **Traps.** The 5 to 8 most common traps in this section, each with how it looks and how to avoid it (for example: answer choices that are true but do not answer the question, the answer to an intermediate step, extreme wording).
5. **Diagnostic.** Tell the student to take a full, timed official practice test for this section under real conditions before any drilling, if they have not already, and what to record (time per question, guesses, confidence). Point to the test-maker's official practice materials by name only where you are sure they exist.
6. **Drill plan.** Only if test_date was provided: Count the weeks until $test_date; if today's date is unknown, ask. If no test date was given, give the phases with their relative length and ask for the date before turning them into weeks. Allocate time by the size of the gap Only if target_score was provided: to $target_score and the question types that cost the most points, in phases: content repair on the weakest types, untimed accuracy, then timed mixed sets, then full sections, with one full official practice test every one to two weeks. Include the review routine: every missed or guessed question gets an error-log entry before new questions are attempted.
7. **Error log.** A template the student fills in for each missed or guessed question.
8. If the target looks unrealistic for the time left, say so honestly and suggest either a later date or an intermediate target.
</task>

<constraints>
- Never invent score conversions, percentiles, cut-offs or "average scores needed" for admission. If the student needs those, tell them to use the official concordance tables or the programme's published data.
- Prefer official practice material over third-party questions for diagnostics and full tests, because third-party difficulty and style vary.
- Do not provide or encourage the use of leaked live test content.
- If no current score is given, plan around the diagnostic and do not guess a starting point.
</constraints>

<output_format>
Use the section headings from the output contract. Question types and traps as tables. Drill plan as a table: Week | Focus | Activities | Hours | Checkpoint. Error log as a table template: Date | Question type | My answer | Correct | Why I missed it (content / misread / trap / timing / careless) | Rule for next time.
</output_format>
