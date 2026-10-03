---
name: write-multiple-choice-questions
description: Writes multiple-choice questions that test understanding, with distractors drawn from real misconceptions, item-writing checks and a rationale for every option. For teachers building quizzes.
license: CC0-1.0
arguments:
  - topic
  - learning_objectives
  - count
  - level
argument-hint: <topic> [learning_objectives] [count] [level]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/write-multiple-choice-questions
  catalog: 2026.1003.1
---

# Write multiple-choice questions

## Inputs

- `topic` (required): The topic or material to assess; pasted content keeps the items aligned to what was taught.
- `learning_objectives` (optional): Optional objectives the items must cover, e.g. "explain why ionic compounds conduct when molten but not solid".
- `count` (optional; default: 10): Number of questions to write.
- `level` (optional): Optional grade or course, e.g. "Grade 8 science", "first-year nursing pharmacology".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A good multiple-choice item can test reasoning, not just recall, and tells the teacher why a student got it wrong, but only if each wrong option is a mistake real students make. Most homemade items leak the answer through cues (the longest option, grammar that fits only one choice, "all of the above") or test trivia. The item-writing guidelines researchers have validated for decades are short and mechanical enough to check every item against.
</context>

<task>
Write $count multiple-choice questions on this materialOnly if level was provided:  for $level.

<material>
$topic
</material>
Only if learning_objectives was provided: 
<objectives>
$learning_objectives
</objectives>

1. **Blueprint.** Map the items to the objectives (or, if none are given, to 3 to 6 objectives you derive from the material and state). Aim for about a third recall and two thirds understanding and application: interpreting a scenario, data, a diagram described in words, or predicting an outcome.
2. **Write each item:**
   - A stem that poses a complete question, answerable before reading the options. Put shared wording in the stem, not repeated in options.
   - One unambiguously correct answer and 2 or 3 distractors (3 or 4 options in total). Each distractor is a specific misconception or a common procedural error, plausible to a student who has not mastered the idea.
   - Options that are similar in length, grammatically parallel, and in a logical order (numbers ascending).
   - No "all of the above", no "none of the above" unless it is genuinely needed, no negatives in the stem unless essential (then bolded: **NOT**), no absolutes like "always" or "never" as giveaways, no clang words repeating the stem in only the key.
3. **Rationale.** For every option: why it is right, or which misconception or error it represents, so the teacher can read results diagnostically.
4. **Check the set.** Verify each key is correct and each distractor is genuinely wrong. Spread the correct answers evenly across letter positions. Make sure no item gives away the answer to another.
</task>

<constraints>
- Items must be answerable from the material and the level; do not test facts outside it.
- If the material is too short to support $count distinct items without trivial or near-duplicate questions, write fewer and say why.
- If a distractor might be defensibly correct under some reading, rewrite it.
- Keep language accessible: test the concept, not reading speed or vocabulary unrelated to the subject.
</constraints>

<output_format>
## Blueprint
A table: Objective | Items | Cognitive level.
## Questions
Numbered items with options A to D (or A to C), no answers marked, so the section can be copied straight into a quiz.
## Answer key and rationales
A table per item: Option | Correct? | Rationale or misconception.
## Item checks
A short table: Item | Objective | Key position | Checks passed (stem complete, cues removed, distractors plausible), and the key distribution across positions.
</output_format>
