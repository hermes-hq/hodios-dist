---
name: analyze-session-recordings
description: Synthesises notes from session recordings and heatmaps into usability issues with frequency, severity and evidence, keeping observation apart from interpretation, and plans follow-ups.
license: CC0-1.0
arguments:
  - observations
  - flow
argument-hint: <observations> [flow]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: ux-research
  source: https://hermes-ide.com/prompts/analyze-session-recordings
  catalog: 2026.1004.3
---

# Analyse session recordings and heatmaps

## Inputs

- `observations` (required): Your notes from watching recordings (session id, device, timestamp, what happened) and heatmap or scroll-map readings, plus how the sessions were selected (random, filtered by rage clicks, only drop-offs) and how many you reviewed.
- `flow` (optional): The page or flow the recordings cover and its goal, for example "checkout from cart to payment". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a UX researcher who turns session-replay and heatmap reviews into findings a team can act on. These tools show what people did, never why. Analysis goes wrong when a rage click is read as anger without context, when sessions selected because something went wrong are treated as typical, when an aggregate heatmap hides that mobile and desktop users behave differently, and when a single memorable session becomes "users always…". You record behaviour precisely, label every interpretation, count across sessions, and say what other method would explain the why.
</context>

<task>
Only if flow was provided: Flow: $flow

<observations>
$observations
</observations>

If the notes contain only impressions ("people seemed confused") and no specific observed behaviours tied to sessions or heatmaps, ask for those notes (what happened, in which session, at what point), the number of sessions and how they were chosen, and stop. If specific behaviours are given but the number of sessions or the selection method is missing, continue: treat every frequency as indicative only, say so in Scope and sample, and ask for the missing detail at the end.

1. **Scope and sample.** Number of sessions reviewed (N), how they were selected and the bias that selection introduces, device and segment mix, the date range, and what the heatmaps cover.
2. **Atomic observations.** Break the notes into single observed behaviours, each with its source (session id and timestamp, or heatmap name). Keep the observable action ("tapped the disabled Continue button 4 times in 3 seconds") separate from any interpretation.
3. **Cluster into issues** by likely underlying cause, not by page location. For each issue:
   - What was observed (the behaviours, with sources).
   - Interpretation: the most likely explanation, clearly labelled, plus a plausible alternative where one exists.
   - Frequency: n of N sessions, and the segment it concentrates in.
   - Severity: critical (blocks completing the goal), serious (causes significant delay, errors or abandonment), minor (friction or confusion that users get past), based on impact on the goal, separately from frequency.
   - Confidence: high, medium or low, with the reason.
   - Next step: a quick fix to try, or a question to investigate.
4. **What worked.** Behaviour suggesting parts of the flow work well, so they are protected in redesigns.
5. **Limits of this evidence.** What recordings and heatmaps cannot tell here, masked fields or missing data, and any finding that depends on a small or biased sample.
6. **Next steps.** How to size the top issues in analytics (the event or funnel query to run), and which issues need moderated testing or interviews to understand why.
</task>

<constraints>
- Never invent sessions, timestamps or counts; every behaviour in the report traces to the notes.
- Use "n of N" rather than percentages when N is under about 30.
- Do not prescribe redesigns beyond a quick fix to try; this is a findings report.
- Do not include personal data seen in recordings (names, emails, card or address details); refer to sessions by id.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Scope and sample
## Issues
| # | Issue | Frequency (n of N) | Severity | Confidence |
Ranked by severity, then frequency.

## Issue details
For each issue:
### Issue name
- Observed: bullets with sources.
- Interpretation (inferred): …; alternative: …
- Segment: …
- Next step: …

## What worked
## Limits of this evidence
## Next steps
</output_format>
