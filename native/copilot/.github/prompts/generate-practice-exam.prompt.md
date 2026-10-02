---
description: Generates a practice exam from course material with mixed question types, a blueprint, an answer key and marking notes for open answers. Use to rehearse before a test.
agent: agent
argument-hint: material question_count difficulty format
---

# Generate a practice exam

<context>
A practice exam is only useful if it samples the material the way a real exam would and if its questions measure understanding rather than test-taking tricks. Weak generated exams over-test trivia, have multiple-choice options where the right answer is obviously the longest, and give no guidance on how open answers are marked, so the student cannot score themselves honestly.
</context>

<task>
Write a ${input:question_count:Number of questions.}-question practice exam, difficulty `${input:difficulty:easy leans on recall, hard on application and analysis, mixed spreads across both.}`, format `${input:format:Question types to use, e.g. "mixed", "multiple choice only", "short answer and one essay", or "like the AP exam".}`, from this material:

<material>
${input:material:The course material the exam should cover. Paste notes, a chapter or a syllabus with content.}
</material>

1. Map the material into topics and estimate each topic's weight from how much the material covers and emphasises it.
2. Build a blueprint: questions per topic in proportion to weight, spread across cognitive levels.
   - `easy`: about 60% recall and understanding, 40% application.
   - `mixed`: about 30% recall, 40% application, 30% analysis or evaluation.
   - `hard`: at least 70% application, analysis or evaluation, using unfamiliar contexts.
3. Write the questions, matching `${input:format:Question types to use, e.g. "mixed", "multiple choice only", "short answer and one essay", or "like the AP exam".}`. With `mixed`, combine multiple choice, short answer, a problem or data question where the subject allows, and one extended response.
   - Multiple choice: one clearly correct answer and three distractors built from real misconceptions; options of similar length and grammar; no "all of the above" or "none of the above"; vary the position of the correct answer.
   - Short answer and extended response: use a command word that says what is expected (state, explain, compare, evaluate, calculate) and show the marks available.
   - Every question must be answerable from the material, stand on its own, and test one clear thing.
4. Assign marks so the total reflects effort, and estimate the time needed (about 1 minute per mark is a sensible default).
5. Write the answer key: for multiple choice, the answer and why each distractor is wrong; for open questions, marking points, acceptable alternatives, how partial marks work, and the common mistakes that lose marks.
</task>

<constraints>
- Only test content in the material. If the material is too thin for ${input:question_count:Number of questions.} good questions, write fewer and say so.
- If the material is only a course name or topic list with no content, ask for the material and stop.
- Keep the exam and the key separate so the exam can be printed or attempted on its own.
- Do not copy questions verbatim from the material's own exercises; adapt them.
</constraints>

<output_format>
## Blueprint
A table: Topic | Weight | Questions (by number) | Cognitive levels. Then: total marks and suggested time.
## Exam
Numbered questions with marks in brackets, e.g. "[3 marks]". Multiple-choice options labelled A to D.
---
## Answer key and marking notes
Numbered to match. For each: the answer, the marking points with marks, and notes on partial credit and common errors.
</output_format>
