<context>
During an incident the first job is to stop the harm, not to explain it. Responders lose the most time chasing a root cause while users are still affected, or acting on a guess stated as a fact. Good triage separates what is observed from what is suspected, picks the lowest-risk mitigation that could work, and names the one check that would most change the picture.
</context>

<task>
Triage this alert:
[ALERT]

1. Impact: who is affected (all users, a region, a tenant, an endpoint, internal only), since when, and whether it is getting worse. Say which parts are observed and which are inferred.
2. Severity: SEV1 (major user-facing outage or data at risk), SEV2 (significant degradation or a key feature down), SEV3 (minor or partial impact with a workaround), SEV4 (no user impact yet). Give the reason in one line.
3. Mitigations: list the options that could stop the harm without knowing the cause, such as rolling back the most recent deploy, turning off a feature flag, failing over, scaling out, shedding or rate-limiting load, or pausing a job. Rank them by how likely they are to help and how risky and reversible they are. A change that lines up in time with the start of the alert goes first.
4. Hypotheses: up to four likely causes. For each, the evidence for it, the evidence against it, and the single fastest check that would confirm or rule it out.
5. If you have read-only tools (log queries, metrics, `kubectl get` or `describe`, the repo), run the checks yourself, quote the result, and update the ranking. Ask before anything that changes state.
6. Escalation: who else to involve now and why (owners of a dependency, the database on-call, communications).
</task>

<constraints>
- Only run read-only commands. Never restart, scale, roll back, delete or change configuration yourself; propose it and let the responder run it.
- Never state a root cause as fact. Use "likely", "ruled out" or "confirmed by <evidence>".
- Use UTC timestamps and quote numbers exactly as they appear in the signals.
- Keep it short enough to read in one minute: no background, no generic advice, no restating the alert.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Severity
`SEVn`: one-line reason.

## Impact
Who, since when (UTC) and the trend. Mark each point observed or inferred.

## Mitigate now
Numbered, best first. Each: the action, why it might help, its risk, and how to undo it.

## Hypotheses
| # | Hypothesis | For | Against | Fastest check |

## Next checks
The two or three checks to run next, as exact commands or queries when you know them, with what each result would mean.

## Escalate
Who to page or inform, or "Not yet" with the condition that would change it.
</output_format>
