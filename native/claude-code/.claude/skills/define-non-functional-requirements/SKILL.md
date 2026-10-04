---
name: define-non-functional-requirements
description: Writes measurable non-functional requirements for a feature, covering availability, latency, throughput, security, privacy, accessibility and operability, each with a target, verification and cost.
license: CC0-1.0
arguments:
  - feature
  - users_and_scale
  - regulatory_context
  - existing_slos
argument-hint: <feature> [users_and_scale] [regulatory_context] [existing_slos]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product
  source: https://hermes-ide.com/prompts/define-non-functional-requirements
  catalog: 2026.1004.2
---

# Define non-functional requirements

## Inputs

- `feature` (required): The feature or system and what users do with it.
- `users_and_scale` (optional): Who uses it, how many, where, on which devices, and expected peaks or growth.
- `regulatory_context` (optional): Laws, standards or contracts that apply, for example GDPR, HIPAA, PCI DSS, WCAG level required by contract, data residency.
- `existing_slos` (optional): Current SLOs, platform defaults or targets of the systems this feature depends on.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Non-functional requirements are where specs are vaguest and where systems most often disappoint: "fast", "secure", "highly available" and "scalable" cannot be built, tested or traded off. A useful requirement names the quality, the scope it applies to, a measurable target with the percentile or window, how it will be verified, and what it costs. Targets also have to be consistent with the dependencies: a feature cannot be more available than the services it calls synchronously, and every extra nine roughly multiplies effort.
</context>

<task>
Write the non-functional requirements for:

<feature>
$feature
</feature>

Only if users_and_scale was provided: 
Users and scale: $users_and_scale
Only if regulatory_context was provided: 
Regulatory and contractual context: $regulatory_context
Only if existing_slos was provided: 
Existing SLOs and dependency targets: $existing_slos

1. Identify the user journeys and operations that matter most and the quality attributes relevant to them. Consider availability, latency, throughput and capacity, scalability, durability and data retention, recovery (RPO and RTO), security, privacy, accessibility, compatibility (browsers, devices, OS versions, API versions), operability (observability, deployability, rollback), maintainability and cost. Skip attributes that truly do not apply and say why in one line.
2. For each requirement write:
   - an id (NFR-01, NFR-02…) and the attribute;
   - the scope: which operation, journey or component;
   - a measurable target with its unit, percentile and window, for example "p95 under 300 ms for search requests measured at the load balancer over 28 days", "99.9% of checkout requests succeed per 30 days", "WCAG 2.2 AA for all customer-facing screens";
   - the verification method: load test, synthetic check, SLO dashboard, security review or penetration test, accessibility audit, restore drill, or contract test;
   - the rationale, tied to users, the business or a regulation;
   - the cost or design implication of meeting it.
3. Check consistency: compare availability and latency targets with the dependencies' targets, show the arithmetic for serial dependencies, and flag targets that are not achievable as stated.
4. For regulatory items, state what the regulation typically requires as a requirement to confirm with the compliance or legal owner, not as legal advice.
5. Propose a sensible target where the input gives none, mark it as proposed, and give the cheaper and the stricter alternative so the owner can choose.
</task>

<constraints>
- Every requirement must be testable. Replace words such as fast, secure, scalable, robust and user-friendly with numbers or named standards.
- Do not invent current performance figures, user counts or dependency SLOs. Mark every number that was not given as proposed or assumed.
- Prefer a few requirements that matter over an exhaustive checklist; at most about 15.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Summary
The three to five requirements that will most shape the design, in one line each.
## Requirements
Table: id, attribute, scope, target, verification, rationale, status (given, proposed or assumed).
## Trade-offs and cost
Bullets: what meeting the stricter targets would require, and the consistency checks against dependencies with arithmetic.
## Not specified on purpose
Attributes left out and why.
## Open questions
Numbered, each with who should answer it.
</output_format>
