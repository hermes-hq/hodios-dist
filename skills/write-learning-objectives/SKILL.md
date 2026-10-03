---
name: write-learning-objectives
description: Writes measurable learning objectives with Bloom verbs, conditions and criteria, each aligned to an assessment method that would show mastery. Use when planning a lesson, module or course.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: course-design
  source: https://hermes-ide.com/prompts/write-learning-objectives
  catalog: 2026.1003.2
---

# Write measurable learning objectives

## Inputs

- [TOPIC] (required): The content or unit the objectives cover, optionally with the goal behind it.
- [AUDIENCE] (optional): Optional audience and level, e.g. "Grade 6", "nursing students in year 2", "new sales hires".
- [COUNT] (optional; default: 5): Number of objectives.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
An objective is useful only if you could watch a learner and decide whether they have met it. "Understand", "know", "appreciate" and "be familiar with" fail that test, so do objectives that describe what the teacher will do ("cover the causes of…"). A measurable objective names the learner, one observable verb at the intended cognitive level, the content, and where it matters the conditions and the standard. It also points straight to how it will be assessed.
</context>

<task>
Write [COUNT] learning objectives for the topic belowOnly if [AUDIENCE] was provided: , for [AUDIENCE].

<topic>
[TOPIC]
</topic>

1. Identify what someone who has mastered this topic can do that a novice cannot. Use that as the source of the objectives, not the list of content.
2. Choose cognitive levels suited to the audience and topic, using Bloom's revised taxonomy (remember, understand, apply, analyse, evaluate, create). Spread the objectives across levels, with most at apply or above unless the audience is new to the field.
3. Write each objective as: "By the end, learners will be able to [verb] [content] [condition, if relevant] [criterion, if relevant]."
   - One verb per objective. No "understand", "know", "learn", "appreciate", "be aware of".
   - Use a verb that matches the level and can be observed: identify, explain, calculate, compare, diagnose, justify, design, critique.
   - Add a condition ("given a patient case", "using a calculator") or criterion ("with no more than one error", "within 10 minutes") when it changes what mastery means.
4. For each objective, give the assessment method that would show it and the specific evidence a marker would look for. The method must match the verb: "design" is assessed by making something, not by a multiple-choice question.
5. Check the set: no two objectives overlap, together they cover the topic's core, and each is achievable for this audience.
</task>

<constraints>
- If the topic is too vague to write measurable objectives for, ask up to two questions about the goal and the audience, then stop.
- Keep the topic's terminology, and keep objectives to one sentence each.
- If [COUNT] is too many for a narrow topic, write fewer and say so instead of padding with trivial recall objectives.
</constraints>

<output_format>
## Objectives
A table: # | Objective | Bloom level | Assessment method | Evidence of mastery.
## Notes
Up to 3 bullets: coverage gaps, assumptions about the audience, and any objective that needs a resource or condition the teacher should confirm.
</output_format>
