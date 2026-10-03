---
name: audit-dependencies
description: Triages dependency scan findings by reachability and exploitability, gives the upgrade path, and justifies anything safe to defer. Use when a scanner reports more than the team can fix at once.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: security
  source: https://hermes-ide.com/prompts/audit-dependencies
  catalog: 2026.1003.1
---

# Triage dependency vulnerabilities

## Inputs

- [SCAN_OUTPUT] (required): Output of the dependency scanner (npm audit, pip-audit, OSV-Scanner, Trivy, Snyk, Dependabot alerts or similar).
- [MANIFEST] (optional): The manifest and lockfile excerpts, and notes on how the vulnerable packages are used, if known.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Scanners rank by CVSS base score, which ignores whether your code can reach the vulnerable function, whether the package ships to production at all, and whether anyone is exploiting it. Teams either drown in hundreds of "critical" findings or bump everything blindly and break the build. Good triage fixes what is reachable and exploitable first, finds the smallest upgrade that clears the most findings, and records a defensible reason for everything it defers.
</context>

<task>
Triage this scan:
[SCAN_OUTPUT]
Only if [MANIFEST] was provided: 
Manifest and usage notes:
[MANIFEST]

1. Deduplicate: group findings by package and installed version, since one vulnerable version often appears through several paths.
2. For each group, establish: direct or transitive (and through which parent), runtime or development/build-only, the vulnerable function or condition as the advisory describes it, and whether the code plausibly reaches it with attacker-controlled input. If reachability depends on code you have not seen, say exactly what to check.
3. Weigh exploitability: public exploit, listing in a known-exploited catalogue, or exploit prediction scores. You cannot query these databases live; use what the scan provides and tell the user which to look up.
4. Assign a decision: fix now (reachable or known-exploited in runtime code, or a malicious or typosquatted package), fix this cycle, defer with justification, or not affected.
5. Find the upgrade path: the minimal fixed version, whether it is within the current semver range (a lockfile refresh) or a major bump, and for transitive issues whether to bump the parent or use an override or resolution (with its risk). If no fix exists, give a mitigation or an alternative package.
6. Order the upgrades to minimise churn: one change that clears several findings comes first.
</task>

<constraints>
- Do not invent advisory details, CVSS scores or fixed versions that are not in the scan. When the scan lacks them, name the advisory to look up.
- Every deferral needs a reason in VEX terms (for example "vulnerable code not in execute path", "component not present at runtime") plus a re-review date.
- A malicious-package finding is always "fix now": remove it and treat the environment as possibly compromised.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
## Summary
Counts: fix now, fix this cycle, deferred, not affected.
## Triage
A table: package, installed version, advisory, severity (scanner), runtime or dev, reachable (yes/no/unknown), decision, fixed version.
## Upgrade plan
Numbered commands or manifest edits in order, each with the findings it clears and its breaking-change risk.
## Deferred
Each deferral with its VEX justification and re-review date.
## Verify
Re-run the scanner, run the tests, and check the specific behaviours that a major bump could change.
</output_format>
