<context>
Large epics stall because they are split by technical layer ("build the database", "build the UI"), so nothing works end to end until the very last ticket. Vertical slices cut through every layer and deliver something a user or tester can see, so the team learns early, can ship partway, and can stop when enough value is delivered.
</context>

<task>
Break down this epic: [EPIC]
Largest acceptable item: 2 days of work for one person.

1. State the goal in one sentence and the scope: what is in, and what is explicitly out.
2. Find the walking skeleton: the thinnest end-to-end path that proves the main flow works. Make it slice 1.
3. Add slices that each grow the working system, splitting by workflow step, business rule, data variation, happy path then error paths, or user type. Each slice must be independently testable and, where possible, shippable behind a flag.
4. Give every slice a one-line acceptance check that a tester could verify, its dependencies on other slices, and a relative size (S, M or L, where L is at most 2 days of work for one person). Split anything bigger.
5. Where an unknown blocks sizing or ordering, add a time-boxed spike with the question it must answer.
6. Order the slices so that risk and learning come first and the most valuable behaviour arrives early.
</task>

<constraints>
- No layer-only items ("set up the database", "build the API") unless something truly cannot be sliced; then say why.
- At most 15 slices. If the epic needs more, propose how to split the epic itself and break down only the first part.
- Do not invent requirements. Anything you had to assume goes under Risks and open questions.
- Each slice title starts with a verb and names user-visible behaviour.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Goal and scope
One goal sentence, then "In:" and "Out:" bullets.
## Slices
Table in delivery order: #, slice, acceptance check, depends on, size.
## Spikes
Bullets: question, time box, which slices it unblocks. Or "None".
## Risks and open questions
Numbered.
</output_format>
