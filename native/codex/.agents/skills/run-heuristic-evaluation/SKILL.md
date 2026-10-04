---
name: run-heuristic-evaluation
description: Evaluates a flow step by step against Nielsen's ten usability heuristics and returns located issues with severity ratings and concrete fixes. Use for a fast expert review before or between user tests.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: ux-research
  source: https://hermes-ide.com/prompts/run-heuristic-evaluation
  catalog: 2026.1004.0
---

# Run a heuristic evaluation

## Inputs

- [FLOW] (required): The flow to evaluate, as screenshots in order or a step-by-step description of each screen, its content and what happens on each action. State the user's goal if you know it.
- [PLATFORM] (optional): Platform and context, e.g. "iOS app", "desktop web, enterprise admins". Optional; it decides which platform conventions apply.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A heuristic evaluation is an expert walking through an interface with a goal in mind and naming where it breaks recognised usability principles. Done badly it becomes a checklist exercise: one vague comment forced under each heuristic, no location, no severity, no fix. Done well it is a ranked list of specific problems, each tied to a step in the flow and a principle, that a designer can act on the same day.
</context>

<task>
Evaluate this flowOnly if [PLATFORM] was provided:  on [PLATFORM]:

<flow>
[FLOW]
</flow>

Nielsen's ten heuristics:
H1 Visibility of system status. H2 Match between the system and the real world. H3 User control and freedom. H4 Consistency and standards. H5 Error prevention. H6 Recognition rather than recall. H7 Flexibility and efficiency of use. H8 Aesthetic and minimalist design. H9 Help users recognise, diagnose and recover from errors. H10 Help and documentation.

1. State the user's goal and the steps you will walk. If the goal is not given, infer it and say so.
2. Walk the flow one step at a time as that user. At each step ask: do I know where I am and what just happened, what I can do next, how to undo it, and what the words mean?
3. Record each problem with its location (step and element), the heuristic or heuristics it violates, what goes wrong for the user, and a concrete fix.
4. Rate severity on Nielsen's 0 to 4 scale: 0 not a problem, 1 cosmetic, 2 minor, 3 major (important to fix), 4 catastrophe (must fix before release). Weigh how often it occurs, how much it hurts when it does, and whether users can get past it once they know.
5. Apply the platform's conventions under H4 (Apple Human Interface Guidelines for iOS and macOS, Material Design for Android, common web patterns) when the platform is known.
6. Note states the input does not show (errors, empty, loading, slow network) as gaps to check, not as found problems.
7. If the input is too sparse to evaluate (a single screen name, no description of content or actions), ask for screenshots or a fuller description and stop.
</task>

<constraints>
- Report only real problems. Do not force a finding under every heuristic; an empty heuristic is fine.
- One finding per problem. If one problem violates two heuristics, list both on one row.
- Describe what you can see or what the description states. Mark anything inferred from a description rather than seen as "inferred".
- Accessibility problems you notice can be reported, but say that a heuristic evaluation is not an accessibility audit.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Scope
Goal, platform, steps walked, assumptions.
## Findings
| # | Step / element | Heuristic(s) | Problem for the user | Severity (0-4) | Fix |
Sorted by severity, highest first.
## Coverage
Count of findings per heuristic, and states not shown that still need checking.
## Top fixes
The 3 changes that would remove the most severe problems, in order.
## Limitations
One evaluator finds only part of the problems (a third is typical); recommend 3 to 5 evaluators and a usability test to confirm severity.
</output_format>
