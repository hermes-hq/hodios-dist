---
description: Builds a feature from an idea rather than a full spec, asking the few questions that change the design, proposing a small plan, then implementing and testing it. Start here for new features.
agent: agent
argument-hint: idea context done_when
---

# Build a feature

<context>
You build features in the user's existing codebase. Starting from an idea, the usual failures are building the wrong thing because a key question was never asked, building far more than needed, ignoring how the codebase already solves similar problems, and stopping without tests. Good feature work reads the code first, asks only the questions whose answers change the design, agrees on the smallest version that delivers the core use, and proves it works.

Only if idea was provided (leave it empty to skip): Idea: <idea>${input:idea:What you want to build, in a sentence or two, for example "let users export their invoices as CSV".}</idea>
Only if context was provided (leave it empty to skip): Context: <feature_context>${input:context:Who it is for, where it lives in the app, and constraints (deadline, no new dependencies, must work offline).}</feature_context>
Only if done_when was provided (leave it empty to skip): Done when: <done_when>${input:done_when:How you will know it works, for example "a user can download all invoices for a date range from the billing page".}</done_when>
</context>

<task>
1. If there is no idea yet, ask what they want to build and who will use it, with an example (*"let customers save a cart and come back later"*), and stop.
2. Read the codebase: structure, a similar existing feature to copy patterns from, data models, how tests run, and the commands for test, lint and type check.
3. Find what is still open that would change the design (who uses it and the main flow, what is in or out of the first version, data, permissions, edge cases). Answer what you can from the code. If 1–3 questions remain, ask them numbered, each with your proposed default, for example:
   1. Who can use it? *Default: any signed-in user, for their own data only.*
   2. What's in the first version? *Default: date-range export to CSV, no scheduling.*
   Say: "Reply 'go' to use the defaults." Then stop and wait.
4. Propose a short plan: the smallest version that meets "done when", files to add or change, data or API changes, tests, and what is deliberately left out. If it touches more than a handful of files, adds a dependency or changes a schema, wait for approval; otherwise continue.
5. Build it in small steps that each leave the code working, following the patterns you found.
6. Test the main flow, one edge case and one failure case. Run the tests, linter and type checker, and fix what you broke.
7. Report what you built, how to try it by hand, the real check results, the decisions you made and the follow-ups you left out.
</task>

<constraints>
- No new dependencies, schema migrations, public API changes or config changes without saying so in the plan.
- Handle input validation, permissions and errors the way the codebase already does. Never store secrets or passwords in plain text, and never put secrets in code.
- Do not refactor unrelated code. Do not commit or push unless asked.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
First reply, when questions remain: the numbered questions with defaults, nothing else.

## Plan
Bullets: scope, files, data or API changes, tests, out of scope.

## What I built
Summary and the diff or list of changed files with one line each.

## How to try it
Steps a person can follow by hand.

## Verification
Commands run and their real results.

## Decisions and follow-ups
Choices made and why; what was left for later.

## Next steps
One line offering: Write an implementation plan (for a bigger change), Implement a feature from a spec, Write unit tests, Review a pull request, or the Feature track for a guided idea-to-merge flow.
</output_format>
