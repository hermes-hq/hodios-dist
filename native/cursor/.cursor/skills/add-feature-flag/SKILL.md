---
name: add-feature-flag
description: Wraps new behaviour behind a feature flag with a safe default, a kill switch, tests for both paths and a cleanup ticket. Use when shipping a risky change incrementally.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/add-feature-flag
  catalog: 2026.1004.2
---

# Put a change behind a feature flag

## Inputs

- [CHANGE] (required): The new behaviour to put behind the flag, as a description or a diff.
- [FLAG_SYSTEM] (optional; default: existing system or env var): Flag system to use, for example LaunchDarkly, Unleash, OpenFeature, a config table or an env var.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A flag is only a safety net if turning it off really restores the old behaviour, and only cheap if it is removed once the rollout ends. Flags go wrong when the default is the new code, when an outage of the flag service flips everyone to the untested path, when the check is scattered across a dozen `if` statements that drift apart, when a schema change makes the old path impossible, or when nobody owns the removal and the flag lives for years.
</context>

<task>
Put this change behind a feature flag:

[CHANGE]

Flag system: [FLAG_SYSTEM] (with the default, use the flag system the repo already has; if it has none, use an environment variable read through the existing config layer).

1. Find how the repo already defines, names, reads and tests flags. Follow that exactly, including the naming convention.
2. Classify the flag (release toggle, ops kill switch, experiment or permission) and choose its lifetime from that.
3. The default and every failure mode, such as the flag service being unreachable or the flag missing, must evaluate to the **old** behaviour.
4. Evaluate the flag once per request or unit of work, at the highest sensible point, and branch there. Do not scatter checks through the call tree or evaluate inside hot loops. Pass the decision down if deeper code needs it. For percentage rollouts, evaluate against a stable targeting key (user or account id) so one user does not flip between paths from one request to the next.
5. Keep both paths complete and independently correct. If the change touches persisted data or a schema, make sure both paths can read what the other writes (expand then contract). If they cannot, say so plainly: a flag cannot protect that part.
6. Record which path ran, using the project's logging or metrics conventions, so the rollout can be watched.
7. Tests: the old path with the flag off, the new path with the flag on, and the old path when flag evaluation fails. Reuse the existing test helpers for overriding flags.
8. Run the tests.
</task>

<constraints>
- Do not change the old path's behaviour, even to tidy it.
- Do not use a flag to gate a security fix; say so if the change is one.
- Targeting rules (percentages, user segments) only if the flag system supports them; do not build your own.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Flag
| Name | Type | Default | Evaluated at | Failure behaviour | Suggested expiry |

## Changes
One line per file.

## Tests
One line per test: which path and condition.

## Rollout and kill switch
Numbered steps to enable gradually, the signals to watch, and exactly how to turn it off without a deploy (or a warning if the chosen system needs a deploy).

## Cleanup ticket
Ready to paste: title, owner placeholder, due date placeholder, every code location to delete, and the tests to remove or keep.
</output_format>
