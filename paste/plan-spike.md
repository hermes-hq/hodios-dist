<context>
A spike is a short, time-boxed investigation that buys information, not features. Spikes go wrong when the question is vague ("look into Kafka"), when nobody defines what "done" means, or when the prototype quietly becomes production code. A good spike plan fixes all three before the clock starts.
</context>

<task>
Plan a spike for: [QUESTION]
Time box: 2 days.

1. Rewrite the unknown as one or two answerable questions, each with a yes or no, a number, or a choice between named options as its answer.
2. Name the decision or estimate the answer unblocks, and who makes it.
3. Define exit criteria: the evidence that answers each question, and what result would mean "go", "no go" or "need more data".
4. List the experiments, cheapest and most informative first (reading docs and code, asking someone, a throwaway prototype, a measurement). Give each a share of the time box and what it should show.
5. Add a checkpoint at about half the time box to decide whether to continue, narrow the question or stop.
6. Define the deliverable: a short findings note with the answer, the evidence, the recommendation and what remains unknown.
</task>

<constraints>
- Fit the whole plan inside 2 days. If it cannot be answered in that time, say so and narrow the question instead of stretching the box.
- Prototype code is throwaway by default. Say so in the plan, and list anything that must be rebuilt properly if the answer is "go".
- Do not pre-decide the answer or bias the experiments toward one outcome.
- Do not state facts about tools or products you are unsure of; turn them into things the spike checks.
</constraints>

<output_format>
## Question
The sharpened questions, numbered.
## Decision it unblocks
One or two lines.
## Exit criteria
Bullets: go, no go, need more data.
## Plan
Numbered experiments with time share and expected evidence, plus the checkpoint.
## Deliverable
What the findings note contains.
## Out of scope
Bullets.
</output_format>
