---
name: break-down-big-task
description: Breaks an overwhelming task into concrete steps that each take under an hour, orders them by dependency, flags unknowns and picks the one step to do today. Use when a big task feels impossible.
license: CC0-1.0
arguments:
  - task
  - deadline
argument-hint: <task> [deadline]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: task-management
  source: https://hermes-ide.com/prompts/break-down-big-task
  catalog: 2026.1003.2
---

# Break down a big task

## Inputs

- `task` (required): The big task in your own words, with whatever you know about it - what done looks like, what you have already, what worries you.
- `deadline` (optional): Optional - when it is due and how much time you can give it per day or week, for example "Friday 17:00, about 2 hours a day".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Big tasks stall for predictable reasons: "done" is fuzzy, the first step is unclear or too big, hidden decisions and unknowns block progress, and the whole thing feels like one undivided lump. A good breakdown fixes all four: it defines the finish line, turns the lump into small physical actions, surfaces the unknowns as their own steps, and makes starting today easy.

<task_description>
$task
</task_description>
Only if deadline was provided: 
Deadline and available time: $deadline
</context>

<task>
1. Define done in one or two sentences: the concrete thing that will exist or be true when the task is finished. If the task description is too vague to define done (for example "sort out my life admin"), ask up to three short questions and stop.
2. Break the task into steps. Each step:
   - starts with a physical verb ("Email", "Draft", "List", "Call", "Book"), not "work on" or "think about";
   - takes under 60 minutes; split anything larger;
   - has a rough time estimate in minutes;
   - produces something visible (a list, a draft, a sent message, a decision).
3. Turn every unknown, decision or dependency on another person into its own early step ("Ask Ana which template to use"), because waiting on others is slow and should start first.
4. Order the steps by dependency, then by what unblocks the most. Group them into three to six phases if there are more than ten steps.
5. If a deadline was given, add up the estimates, compare with the available time, and say plainly whether it fits. If it does not, propose what to cut, simplify or ask for.
6. Pick one step to do today: the smallest step that creates momentum or unblocks others. Write a two-minute starter for it (the very first physical move).
</task>

<constraints>
- Use the user's words and details; do not invent requirements, people, tools or deadlines. Mark assumptions as such.
- Estimates are rough and labelled as such; add about 25 percent buffer to the total because people underestimate.
- Keep it to the steps needed for done. Nice-to-haves go under "If you have more time".
- No motivational filler. The breakdown itself is the help.
</constraints>

<output_format>
## Done looks like
One or two sentences.
## Steps
A numbered checklist grouped by phase if needed: `- [ ] Step (estimate)`. Mark steps that wait on someone else with "(waiting)".
## Unknowns
Bulleted questions or decisions, each linked to the step that resolves it.
## Do today
The chosen step, why it comes first, and the two-minute starter.
## If you have more time
Optional extras, one line each.

If a deadline was given, add a one-line capacity verdict after the steps: total estimate with buffer versus time available.
</output_format>
