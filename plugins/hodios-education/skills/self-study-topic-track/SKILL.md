---
name: self-study-topic-track
description: Teaches a new topic in gated steps, from a diagnostic and concept map through explanation, retrieval practice and an application task to a spaced review plan.
license: CC0-1.0
arguments:
  - topic
  - goal
  - hours_per_week
argument-hint: <topic> <goal> [hours_per_week]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: studying
  source: https://hermes-ide.com/prompts/self-study-topic-track
  catalog: 2026.1003.1
---

# Self-study topic track

## Inputs

- `topic` (required): The topic to learn, as specific as possible, for example "Bayes' theorem", "how vaccines train the immune system", "the causes of the 2008 financial crisis".
- `goal` (required): What the learner wants to be able to do afterwards and why, for example "explain it to my team and use it to read A/B test results", "pass the unit test on it next month".
- `hours_per_week` (optional; default: 3): Realistic hours per week for this topic. Sets the size of each session and the review plan.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Teaches $topic so the learner can $goal, the way a good tutor runs a short course for one person: find out what they already know, show how the ideas fit together, explain from there, make them retrieve it rather than reread it, test it on a real task, and schedule reviews so it stays. Each step ends with something the learner does (answer, check, recall, apply) and waits for it; later steps use what earlier ones found instead of starting over. Sessions are sized to $hours_per_week hours a week. Throughout, the assistant states the level of certainty on contested or fast-changing points, never invents sources, and asks when the goal or the learner's background is unclear.

## Steps

Work through these steps in order. Do not skip a gate.

1. diagnose (discover)
2. concept-map (plan)
3. explain (learn)
4. retrieval (verify)
5. apply (build)
6. review-plan (maintain)

### Step 1: Diagnose what the learner already knows

Find the starting point for learning $topic.

1. Restate the goal ($goal) as two to four concrete things the learner will be able to do at the end, each something that can be checked ("calculate a posterior from a 2x2 table", "explain why X causes Y to a colleague"). If the goal is vague, propose these and ask the learner to confirm.
2. Identify the prerequisites the topic depends on and list them.
3. Write a short diagnostic of 6 to 10 questions the learner can answer in about 15 minutes:
   - 2 or 3 on the prerequisites.
   - 3 or 4 on core ideas of the topic itself, so you learn whether they already know some of it.
   - 1 or 2 asking them to explain, in their own words, what they think the topic is about and where they have met it.
   Number them, mix short answers with one or two small problems where the topic allows, and include no answers.
4. Ask them to mark each answer with a confidence from 1 (guess) to 3 (sure) and to answer from memory without looking anything up.

Stop. Wait for the learner's answers.

**Gate:** stop here and wait for the user's approval before step 2 (concept-map).

### Step 2: Map the topic

Mark the diagnostic and lay out how $topic fits together.

1. Mark each diagnostic answer: correct, partly correct or wrong, with a one-line reason. Treat a correct answer marked as a guess as not yet known. Name any misconception you see, kindly and precisely.
2. If a prerequisite is weak, say which and plan a short catch-up on it at the start of step 3, rather than pushing on.
3. Build a concept map of the topic with 8 to 15 concepts: each link labelled with a verb phrase ("is a type of", "causes", "is calculated from", "is limited by"), the core idea at the centre, and the learner's known concepts marked as known. Give it as an indented outline, and as Mermaid if the learner wants a diagram.
4. Propose the learning order: which concepts first, which build on them, and the session plan sized to $hours_per_week hours a week (sessions of 25 to 50 minutes, each with one goal).

Stop. Ask the learner to approve or adjust the map and the order.

**Gate:** stop here and wait for the user's approval before step 3 (explain).

### Step 3: Explain, one concept at a time

Teach the concepts of $topic in the approved order, one session at a time.

1. Start each session by asking one quick recall question about the previous session.
2. For each concept: connect it to something the learner already knows from the diagnostic, explain the core idea in plain language, give one concrete example and one non-example or common confusion, then show a worked example where the topic allows one. Use a diagram described in words or a simple table when it makes a relationship clearer.
3. After each concept, ask the learner one question that makes them use it, not repeat it ("Which of these two cases is an example, and why?"). Wait for the answer, then correct or confirm briefly.
4. Keep each explanation short: what fits in about 10 minutes of reading. If the learner says it is too fast or too slow, adjust the level.
5. Note any concept that took several tries; it gets extra practice in step 4.
6. Flag the boundary of your knowledge: where experts disagree, where details change over time, or where the learner should confirm with a textbook or official source, say so.

Repeat until every concept on the map has been explained, then stop and suggest moving to retrieval practice.

**Gate:** stop here and wait for the user's approval before step 4 (retrieval).

### Step 4: Retrieval practice

Make the learner pull $topic from memory, without notes.

1. Begin with a blank-page recall: ask them to write, from memory, everything they can about the topic in 5 minutes, then compare it with the concept map and list what they missed.
2. Give a set of 8 to 12 mixed questions across all concepts, interleaved rather than grouped by concept, with more weight on concepts that took several tries in step 3. Mix recall, explanation ("why does…"), and small application problems. No hints or answers in the same message.
3. Wait for the answers. Mark each one with the reason. For a wrong answer, give a brief re-explanation and one new question on the same idea.
4. Keep a tracker: Concept | Correct this round | Secure? A concept is secure when answered correctly from memory twice, in different rounds.
5. Offer flashcard lines ("question;answer") for any concept that is not yet secure.

Repeat rounds until most concepts are secure, then stop and ask the learner to move to the application task.

**Gate:** stop here and wait for the user's approval before step 5 (apply).

### Step 5: Apply it to a real task

Test whether the learner can use $topic for their goal: $goal.

1. Design one application task that matches the goal, in a context the learner has not seen in steps 3 and 4. Examples: analyse a short real-world case, solve a multi-step problem, explain the topic to a named audience in 200 words, or critique a flawed explanation you supply.
2. State what a good response must do in 3 to 5 checkable criteria, and the time to spend (about one session).
3. Wait for the learner's attempt. Then give feedback against each criterion: what met it, what fell short, and one specific improvement. Point out where a misconception from earlier steps reappeared.
4. If the attempt shows a concept is still not secure, give a short targeted fix and one more question on it.

Stop. Ask whether the learner is satisfied or wants a second application task, then move to the review plan.

**Gate:** stop here and wait for the user's approval before step 6 (review-plan).

### Step 6: Spaced review plan

Plan how the learner keeps $topic over the coming weeks.

1. Summarise what is secure, what is shaky and the one misconception to watch for, based on steps 4 and 5.
2. Build a spaced review schedule from today: short reviews after about 1 day, 3 days, 1 week, 2 weeks and 1 month, each 10 to 20 minutes and fitted into $hours_per_week hours a week. Shaky concepts get the earlier and extra reviews.
3. For each review, say what to do: blank-page recall against the concept map, 5 to 8 mixed questions you list now, or a short application. Rereading alone is not a review.
4. Give the learner a one-paragraph summary of the topic to compare their recall against, and the flashcard lines for anything not secure.
5. Suggest one next topic that builds on this one and fits the goal, and say why.
