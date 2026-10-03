---
name: choose-branching-strategy
description: Recommends a branching and release strategy such as trunk-based, GitHub flow or release branches for a team's size, cadence and environments, with rules, protections and migration steps.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: git
  source: https://hermes-ide.com/prompts/choose-branching-strategy
  catalog: 2026.1003.0
---

# Choose a branching strategy

## Inputs

- [TEAM] (required): Number of engineers and teams, repo layout (monorepo or many repos), experience with CI and feature flags, and how work is reviewed today.
- [RELEASE_CADENCE] (required): How often you release and how, for example "continuous deploys", "weekly web release", "monthly app store release", "versioned library with LTS".
- [ENVIRONMENTS] (optional): Environments and how code reaches them, for example "dev, staging, production; staging deploys on merge".
- [CONSTRAINTS] (optional): Anything fixed, such as regulated change approval, multiple supported versions in the field, hotfix needs, code host, or long QA cycles.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A branching strategy is a delivery decision disguised as a git decision. Long-lived branches feel safe but delay integration, so merges get bigger, conflicts get worse and releases get riskier; research on delivery performance (the DORA programme) consistently associates trunk-based development with better outcomes. But trunk-based development only works with fast CI, small changes and a way to hide unfinished work. Teams shipping to app stores, supporting several released versions, or under formal change control genuinely need release branches. The right strategy is the simplest one the team's release model and engineering practices can support today, with a path to simpler.
</context>

<task>
Recommend a branching and release strategy for this team.

<team>
[TEAM]
</team>

Release cadence: [RELEASE_CADENCE]
Only if [ENVIRONMENTS] was provided: 
Environments: [ENVIRONMENTS]
Only if [CONSTRAINTS] was provided: 
Constraints: [CONSTRAINTS]

1. Identify the deciding factors: how often and how code reaches production, whether more than one released version must be maintained, whether releases need a stabilisation period, the team's CI speed and test confidence, use of feature flags, and regulatory or approval steps. If a deciding factor is missing, state your assumption.
2. Compare the candidates that fit: trunk-based development (short-lived branches or direct commits, merged at least daily), GitHub flow (feature branches merged to an always-deployable main), trunk plus release branches cut for each release, and Git Flow (develop, release and hotfix branches). Recommend one and say in one line each why the others lose for this team. Recommend Git Flow only when several released versions must be supported in parallel and nothing simpler works.
3. Write the branch rules: branch types and naming, maximum branch lifetime, where branches start and merge, merge method (squash, rebase or merge commit) and why, how unfinished work is hidden (feature flags, branch by abstraction, dark launches), and how environments map to branches or, preferably, to build artifacts promoted between environments.
4. Write the release and hotfix flow step by step: how a release is cut and versioned, how it is tagged, how fixes reach a release branch (fix on main first, then cherry-pick), and how a hotfix goes to production and back to main without regressing.
5. List protections and automation for the code host: required reviews and status checks on main and release branches, linear history if chosen, who may push or force-push, CODEOWNERS, automatic deletion of merged branches, merge queues for busy repos, and release tagging and changelog automation.
6. Write migration steps from the current way of working, in order, with a checkpoint for each: what to change first, how to drain or merge existing long-lived branches, and the practices (CI speed, flags, PR size) that must be in place before shortening branch lifetimes further.
7. Say what would make the team revisit the choice (for example adding a mobile app, a second supported version, or CI getting slower than a set time).
</task>

<constraints>
- Fit the recommendation to the stated release model. Do not recommend continuous trunk deploys for a product released through an app store review without explaining how releases are cut.
- Do not prescribe practices the team cannot support yet; put them in the migration steps as prerequisites.
- Commands and settings must be specific to the code host if one was named, and generic otherwise.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Recommendation
The strategy and the three main reasons, in at most 5 lines, plus a Mermaid gitGraph showing a typical feature, release and hotfix.
## Why not the alternatives
One line per alternative.
## Branch rules
Table: branch type, naming, created from, merged into, lifetime, merge method.
## Release and hotfix flow
Numbered steps for each.
## Protections and automation
Checklist per protected branch.
## Migration steps
Numbered, each with its checkpoint.
## When to revisit
Bullets.
</output_format>
