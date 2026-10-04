---
name: plan-learning-path
description: Builds a week-by-week plan to get productive in a new language, framework or tool, built around hands-on milestones and skipping what the learner already knows. Use when picking up a new stack.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: learning
  source: https://hermes-ide.com/prompts/plan-learning-path
  catalog: 2026.1004.2
---

# Plan a learning path for a technology

## Inputs

- [GOAL] (required): What you want to be able to do, as concretely as possible (for example "ship a small REST API in Go at work").
- [BACKGROUND] (optional): What you already know, such as languages, frameworks and years of experience.
- [HOURS_PER_WEEK] (optional; default: 5): Hours you can spend each week.
- [WEEKS] (optional; default: 4): Number of weeks for the plan.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Experienced developers learn a new stack fastest by building something real while reading just enough, and by mapping new ideas onto what they already know. Generic plans fail them: they re-teach loops and variables, list dozens of links, and end with no working project. A good plan is ordered by what the goal needs, has a concrete thing to build each week, and says how to tell a week is done.
</context>

<task>
Plan how to reach this goal in [WEEKS] weeks at about [HOURS_PER_WEEK] hours a week: [GOAL]
Only if [BACKGROUND] was provided: 
The learner already knows: [BACKGROUND]

1. Restate the goal as observable skills ("can write and test an HTTP handler with middleware", not "knows Go").
2. List what the learner can skip or skim because of their background, and the concepts that will feel familiar but behave differently (for example Go interfaces compared with Java interfaces). Those differences deserve explicit time.
3. Order the topics by what the goal needs first. Leave out topics the goal does not need, and say so.
4. For each week give: the objective, the topics, a hands-on milestone that builds on the previous week, and a "done when" check the learner can verify themselves (a passing test, a deployed endpoint, explaining X without notes).
5. Fit the plan to the hours. If the goal is unrealistic in the time given, say so and propose either a narrower goal or more weeks.
6. End with a small capstone project that exercises the whole goal.
</task>

<constraints>
- Recommend resources by name only when they are well known and official or standard (the language's official tutorial or documentation, the framework guide, a widely used book). Do not invent URLs, course names, authors or editions. If you are not sure a resource exists, describe the kind of resource to look for instead.
- Keep the reading to a minimum each week; most hours go to building.
- Do not assume a paid service or tool unless the goal requires it, and say when it does.
</constraints>

<output_format>
## Target
The observable skills, as bullets.
## Skip
What to skip or skim, and the familiar-looking concepts that differ.
## Plan
A table: week | objective | topics | milestone | done when.
## Capstone
The project, its scope and the skills it proves.
## Resources
Short list, official sources first, each with what to use it for.
</output_format>
