---
name: vet-dependency
description: Checks a third-party package for supply-chain risk, maintenance health, license fit and real need before it is added or upgraded. Use when a PR adds a new dependency or bumps one.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: security
  source: https://hermes-ide.com/prompts/vet-dependency
  catalog: 2026.1004.0
---

# Vet a dependency before adding it

## Inputs

- [PACKAGE] (required): Package name with its ecosystem and version, for example "npm:left-pad@1.3.0" or "pypi:requests==2.32.3". A diff of a manifest or lockfile also works.
- [PURPOSE] (optional): What the project needs the package for.
- [LICENSE_POLICY] (optional): Licenses the project accepts or rejects, for example "permissive only, no GPL or AGPL".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Every dependency runs with the project's privileges and brings its own dependencies along. Typosquats, hijacked maintainer accounts, malicious install scripts and abandoned packages with open vulnerabilities are common ways into a codebase. A short check before adding a package is far cheaper than removing it after an incident.
</context>

<task>
Vet [PACKAGE].
Only if [PURPOSE] was provided: The project needs it for: [PURPOSE]
Only if [LICENSE_POLICY] was provided: License policy: [LICENSE_POLICY]

1. Identity: confirm the exact name against the registry and the source repository it links to. Flag names one edit away from a popular package, a registry entry with no source link, or a source repo that does not match the published package.
2. Install-time behaviour: check for install, preinstall or postinstall scripts, native builds, binary downloads, and any network or file system access at import time.
3. Maintenance: latest release date, release cadence, number of active maintainers, recent ownership or maintainer changes, open security advisories, and whether known vulnerabilities are fixed in the requested version.
4. Footprint: number of transitive dependencies it adds and anything risky among them. In a repo, compare against the lockfile to see what is new.
5. License: the package's license and any transitive license that conflicts with the policy.
6. Need: whether the project already has a dependency or standard library feature that does the job, and how much code the package saves.
Use your tools to look things up. For every fact, say where it came from (registry page, advisory database, repository). If you cannot reach a source, write "not checked" for that item instead of guessing.
</task>

<constraints>
- Never state download counts, dates, versions, advisories or maintainer facts from memory. Only report what you looked up in this session, with its source.
- Do not install, import or run the package to test it.
- Judge the specific version requested, not the package in general.
- A verdict of `reject` needs at least one concrete reason from the evidence.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: `adopt`, `adopt-with-conditions` (state them, for example "pin to 2.3.1"), or `reject`, plus the main reason.

## Evidence
| Check | Finding | Source |
One row each for identity, install scripts, maintenance, advisories, footprint, license and need. Use "not checked" where you could not verify.

## Risks
Bullets, most serious first. "None found" if empty.

## Alternatives
Up to three: a standard library feature, an existing dependency, or a better-maintained package, each with one line on the trade-off. "None needed" if the package is a good fit.
</output_format>
