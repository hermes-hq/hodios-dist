---
name: explain-worked-solution
description: Explains a worked solution to a maths or science problem step by step, why each step is taken and the idea it uses, flags any error, and sets a similar problem to try next.
license: CC0-1.0
arguments:
  - problem
  - solution
  - level
argument-hint: <problem> [solution] <level>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tutoring
  source: https://hermes-ide.com/prompts/explain-worked-solution
  catalog: 2026.1004.0
---

# Explain a worked solution

## Inputs

- `problem` (required): The problem exactly as set, with any diagram described in words and the units.
- `solution` (optional): Optional worked solution to explain, from a textbook, mark scheme or teacher. Without it, the prompt writes and checks its own solution first.
- `level` (required): The learner's level, for example "Year 11", "AP Calculus AB", "first-year engineering". Sets the vocabulary and the methods used.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Students often have the answer to a problem, from a mark scheme or a textbook, and still cannot see how anyone would think of it. Worked solutions show what was done but rarely why that step, at that moment: the decision behind it. Learning from worked examples works when each step is linked to the principle it uses and the cue in the problem that triggers it, and when the learner then tries a similar problem on their own.
</context>

<task>
Explain the solution to this problem for a learner at $level level.

<problem>
$problem
</problem>
Only if solution was provided: 
<solution>
$solution
</solution>

1. Check the solution. Work the problem yourself and verify the answer by an independent route (substitution, units, an estimate, a limiting case). If a solution was supplied and it contains an error or an unjustified step, say exactly where and what the correct step is before explaining anything. If no solution was supplied, write your own clear solution and say it is yours.
2. Break the solution into steps a learner at this level would recognise (merge trivial algebra; split steps that hide a decision).
3. For each step, explain three things: what is done; why this step now, meaning the cue in the problem or the previous line that tells you to do it; and the idea, law or rule it uses, named in terms the learner will meet at their level.
4. Name the key idea: the one step or insight that unlocks the problem, and how to spot problems that need it.
5. List the two or three mistakes students commonly make on this kind of problem and how the solution avoids them.
6. Write one similar problem that uses the same key idea in a different surface form (different context or numbers, same structure). Do not give its answer; offer to check the learner's attempt.
</task>

<constraints>
- Use only methods and notation appropriate to $level. If the supplied solution uses a method beyond that level, explain it gently and mention the method the learner is expected to use.
- Never explain an incorrect step as if it were correct.
- Keep each step's explanation to two or three sentences. Write maths in the notation the problem uses (plain text or LaTeX).
- If the problem is missing information needed to solve it, say what is missing and stop.
</constraints>

<output_format>
## Check
One line: the solution is correct, or where it goes wrong and the fix. Say if the solution is your own.
## Step by step
A table: Step | What happens | Why this step now | Idea used.
## The key idea
2 to 3 sentences.
## Where people go wrong
Bullets.
## Try this next
The new problem, then: "Send me your attempt and I'll check it."
</output_format>
