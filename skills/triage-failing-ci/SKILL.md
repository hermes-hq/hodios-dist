---
name: triage-failing-ci
description: Finds the first real error in a failing CI log, classifies the failure as caused by the change, flaky, environment drift or already broken, and names the next action. Use when a pipeline turns red.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: debugging
  source: https://hermes-ide.com/prompts/triage-failing-ci
  catalog: 2026.1003.0
---

# Triage a failing CI build

## Inputs

- [CI_LOG] (required): The failing job's log, or a link to the CI run if you can fetch it.
- [CHANGE] (optional): The diff, PR or commit range that triggered the run, if known.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A red build is a question with a few common answers: the change broke something, a test is flaky, the environment drifted (a new dependency release, a new runner image, an expired credential, a rate limit), or the base branch was already broken. The answer decides who acts and how. CI logs bury the first real error under cascading failures and noisy setup output.
</context>

<task>
Triage this CI failure:
[CI_LOG]
Only if [CHANGE] was provided: 
Triggering change:
[CHANGE]
1. Find the first real error: the earliest failure that the later ones follow from. Skip warnings, deprecation notices and failures that only happen because an earlier step failed.
2. Classify the failure:
   - **change**: the error is in code, tests or config the change touched, or plainly follows from it.
   - **flaky**: timing, ordering or network-dependent failure, unrelated to the change. Look for timeouts, connection resets, port conflicts and tests that touch time or randomness.
   - **environment**: dependency versions resolved differently than before, a runner or image update, missing secrets, quota or rate limits, full disks.
   - **pre-existing**: the same failure is on the base branch. Check the base branch's recent runs or history if you can.
3. Give the evidence for the classification and what would change your mind.
4. Name the next action and who should take it: fix the code (with the likely location), rerun with a reason, pin a dependency, or report an infrastructure issue.
</task>

<constraints>
- Quote the first real error exactly, with its step name and line in the log if available.
- Recommend a rerun only for **flaky** or transient **environment** failures, and say why. Never recommend rerunning a deterministic failure.
- Do not recommend disabling or skipping a test unless the test itself is proven to be broken, and then say how to track re-enabling it.
- If the log is truncated before the error, say so and say which part of the log you need.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Classification
`change`, `flaky`, `environment` or `pre-existing`, with confidence (high, medium, low).
## First real error
The quoted error, its job and step.
## Evidence
Bullets supporting the classification, and one line on what would change it.
## Next action
One or two concrete steps, with the likely file or setting to look at.
</output_format>
