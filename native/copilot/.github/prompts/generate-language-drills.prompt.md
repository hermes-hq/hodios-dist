---
description: Generates a mixed set of cloze, transformation and translation drills for one grammar point, graded by level, with an answer key. Use to practise a rule after learning it.
agent: agent
argument-hint: grammar_point target_language level count native_language
---

# Generate grammar drills

<context>
You write practice material for learners of ${input:target_language:Language being practised.}. Good drills move from controlled to freer use, test only the target point, and include a few items where the point does not apply, because knowing when not to use a form is half of learning it. Items with two defensible answers, obscure vocabulary or the same sentence frame repeated teach very little.

Grammar point: ${input:grammar_point:The grammar point to drill (for example "passé composé with être", "Russian genitive plural").}
Learner level (CEFR): ${input:level:Learner's CEFR level; controls vocabulary and sentence complexity.}
Number of items: ${input:count:Total number of drill items.}
Learner's first language: ${input:native_language:Learner's first language; used for the translation items and the instructions.}
</context>

<task>
1. State in one line how you are interpreting the grammar point. If the name could mean several things, choose the use most relevant at ${input:level:Learner's CEFR level; controls vocabulary and sentence complexity.}.
2. Split the ${input:count:Total number of drill items.} items into three parts, in this order:
   - Part A, cloze (about 40%): a sentence with one gap and the base form in brackets.
   - Part B, transformation (about 30%): rewrite a sentence following an instruction (change the tense, make it negative, combine two sentences, replace the noun with a pronoun).
   - Part C, translation from ${input:native_language:Learner's first language; used for the translation items and the instructions.} (about 30%): short sentences that force the target structure.
3. Make about one item in five a contrast item, where a neighbouring form is correct instead. Do not label which ones.
4. Vary the vocabulary, subjects and contexts; keep all vocabulary at or below ${input:level:Learner's CEFR level; controls vocabulary and sentence complexity.}.
5. Write the answer key: the answer, any accepted alternatives, and a reason of at most 12 words for each item.
</task>

<constraints>
- Each item must have one correct answer, or every accepted alternative must be listed in the key.
- Sentences must be natural and plausible; no trick questions and no rare exceptions unless the level is C1–C2.
- Instructions for each part are in ${input:native_language:Learner's first language; used for the translation items and the instructions.} and one line long.
- Check every answer against the rule before writing the key. If a sentence turns out ambiguous, rewrite it.
</constraints>

<output_format>
Interpretation: one line.
## Part A
Instruction, then numbered items.
## Part B
Instruction, then numbered items continuing the numbering.
## Part C
Instruction, then numbered items continuing the numbering.
## Answer key
Numbered: answer · alternatives if any · reason.
</output_format>
