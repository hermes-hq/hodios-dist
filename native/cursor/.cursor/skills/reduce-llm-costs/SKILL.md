---
name: reduce-llm-costs
description: Cuts an LLM feature's cost and latency through prompt trimming, caching, model routing, batching and output limits, each paired with the quality check that proves nothing regressed.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: ai-ml
  source: https://hermes-ide.com/prompts/reduce-llm-costs
  catalog: 2026.1004.1
---

# Reduce LLM costs and latency

## Inputs

- [USAGE_DATA] (required): Usage numbers - requests per day, input and output tokens per request (averages and p95), cached tokens, models used, retries, monthly bill, and latency percentiles. A sample request is very helpful.
- [FEATURE_DESCRIPTION] (required): What the feature does, how a user action turns into model calls, what goes into each prompt (system prompt, history, retrieved documents, tool definitions) and whether responses must be real time.
- [QUALITY_BAR] (optional): How quality is measured today (eval set, user ratings, acceptance rate) and how much regression is acceptable, if any.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
LLM bills usually grow from a few causes: input tokens repeated on every call (long system prompts, tool definitions, full chat history, too many retrieved chunks), a large model used for every request including easy ones, output longer than anyone reads, retries and duplicate calls, and real-time calls for work that could wait. Most savings are safe, but some quietly lower quality, which no one notices until users do. Every change therefore needs a check that would catch a regression before it ships.
</context>

<task>
Reduce the cost and latency of this feature:
[FEATURE_DESCRIPTION]

Usage data:
[USAGE_DATA]
Only if [QUALITY_BAR] was provided: 

Quality bar: [QUALITY_BAR]

1. Build the cost model from the data: calls per user action, input tokens split by part (system prompt, tool definitions, history, retrieved context, user input), output tokens, cached tokens, retries, and the model behind each call. Show which parts make up most of the spend and most of the latency. Where a split is not in the data, estimate it from the sample request and label it as an estimate.
2. Generate candidate changes from these levers, keeping only the ones the data supports:
   - Remove waste: duplicate or unnecessary calls, retries on non-retryable errors, unused tool definitions, dead instructions.
   - Prompt caching: reorder prompts so the stable part (instructions, tool definitions, fixed documents) comes first and the variable part last, then enable the provider's prompt caching. Check the provider's minimum cacheable length and cache lifetime against the traffic pattern.
   - Trim context: fewer or better retrieved chunks, history summarised or windowed, shorter instructions that say the same thing.
   - Limit output: a maximum output length, a compact format (structured output instead of prose when a program reads it), no restating the input.
   - Route by difficulty: send easy requests to a smaller, faster model and escalate on low confidence or failed validation; say how a request is classified.
   - Batch: move work that does not need an immediate answer to the provider's batch interface or an off-peak queue.
   - Cache responses: exact-match caching for repeated requests; semantic caching only where a near-duplicate answer is acceptable.
   - Fine-tuning or distillation into a smaller model: last, only if the eval shows the smaller model cannot reach the bar with prompting.
3. For each change, estimate the saving with the arithmetic shown (tokens times calls times price), its effect on latency, the quality risk (none, low, medium, high), and the effort.
4. Pair each change with the quality check that must pass before it ships: an offline run on the eval set with a threshold derived from the quality bar, a side-by-side comparison on sampled real traffic, or a shadow or A/B rollout with the metric to watch. If no eval set exists, make building a small one the first change and explain why.
5. Order the changes by saving per unit of quality risk and effort, and give a rollout sequence that changes one thing at a time so each saving and each regression can be attributed.

If prices are not in the usage data, do not quote any: use symbols (price per million input tokens, and so on) and show the formula. If the usage data is too thin to find where the money goes, say what to measure first and how.
</task>

<constraints>
- Never recommend a change that lowers quality without naming the risk and the check. "Use a cheaper model" alone is not a recommendation.
- Do not invent numbers. Every saving traces back to the usage data or an estimate labelled as one.
- Name providers only as examples; describe caching, batching and routing in general terms with what to check in the provider's documentation.
- Keep user-facing behaviour the same unless the change is listed as a product decision for the owner.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Where the money goes
Table: component | tokens per call | calls per day | share of cost | share of latency.

## Ranked changes
Table: # | change | estimated monthly saving | latency effect | quality risk | effort.

## Change details
One subsection per change: what to do, the arithmetic, and the quality check with its pass threshold.

## Rollout
Numbered order, one change at a time, with the metric to watch after each.

## Monitoring
The cost, latency and quality metrics to track per request and the alert thresholds.

## Missing data
What would sharpen the estimates and how to collect it.
</output_format>
