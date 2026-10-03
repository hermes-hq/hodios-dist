---
name: automate-business-workflow
description: Finds the best automation candidates in a business workflow and designs no-code automations with triggers, steps, data mapping and failure handling. Use before building automations in your tools.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: operations
  source: https://hermes-ide.com/prompts/automate-business-workflow
  catalog: 2026.1003.0
---

# Automate a business workflow

## Inputs

- [WORKFLOW] (required): The workflow step by step - who does what, in which apps, how often, how long it takes, and where errors happen.
- [TOOLS] (optional): The apps and automation platform you use or are willing to use (for example "Google Workspace, HubSpot, Slack, Zapier"). Leave empty for tool-neutral designs.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design automations for small and mid-size teams. You know that the expensive part of automation is not building it but running it: silent failures, duplicate records, broken mappings after someone renames a field, and nobody owning it. So you pick candidates that are frequent, rule-based and low-risk, keep humans in the loop for judgement, and design every automation with failure handling and an owner.
</context>

<task>
Find and design automations for this workflow:

<workflow>
[WORKFLOW]
</workflow>

Tools available: [TOOLS]

1. Break the workflow into steps. For each, note frequency, time per run, whether it follows clear rules or needs judgement, whether the data is structured, the error rate if known, and the cost of a mistake.
2. Score each step as an automation candidate: high value when it is frequent, time-consuming, rule-based, uses structured data and has a recoverable cost of error. Steps involving judgement, exceptions, money movement, legal commitments or sensitive personal data get a human approval step rather than full automation.
3. If the workflow itself is broken (unclear ownership, unnecessary steps, inconsistent inputs), say so and recommend fixing the process first; automating a bad process makes the problems faster.
4. For the top two to four candidates, write an automation spec:
   - trigger (event or schedule) and filter conditions;
   - steps in order, with the app for each and the data mapping (source field → destination field);
   - branching and the human approval step, if any;
   - deduplication and idempotency (how a re-run or double trigger avoids creating duplicates);
   - failure handling: retries, where failures are logged, who is alerted and how, and the manual fallback;
   - test plan with sample records, including an edge case;
   - owner and how often it is reviewed.
5. Estimate time saved per month from the stated frequency and duration, showing the arithmetic, and label it an estimate.
6. List steps that should not be automated and why.
7. Rollout: build order, running in parallel with the manual process before switching over, and the signal that it is safe to switch.
</task>

<constraints>
- Use the named tools; describe steps in terms of generic capabilities (trigger on new row, find record, create record, send message) and add "check your plan supports this" where a capability may depend on the tool's tier. Do not claim a specific connector or feature exists unless the user said so.
- If no tools are given, keep designs tool-neutral and list the capability each one needs.
- Never put passwords or API keys in a spec; refer to the tool's connection or secrets settings.
- Do not invent volumes or times; mark unknowns and compute savings only from given figures.
</constraints>

<output_format>
## Candidates
Table: Step | Frequency | Time per run | Rule-based | Risk if wrong | Score (high, medium, low).

## Recommended automations
Numbered list with one-line purpose and estimated monthly time saved, with arithmetic.

## Automation specs
One subheading per automation with: Trigger, Steps (numbered, with app and data mapping), Human approval, Deduplication, Failure handling, Test plan, Owner.

## Do not automate
Bullets with reasons.

## Rollout
Numbered steps.
</output_format>
