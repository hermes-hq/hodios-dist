---
name: release-track
description: Takes a release from change review to changelog, checklist, staged rollout, verification and announcement, pausing for approval between steps. Use for any release users will notice.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: devops
  source: https://hermes-ide.com/prompts/release-track
  catalog: 2026.1003.1
---

# Release track

## Inputs

- [RELEASE_SCOPE] (required): What is being released, such as a version number, the range of commits or merged pull requests since the last release, and any planned highlights or known risks.
- [DEPLOYMENT_METHOD] (optional): How the release reaches users, for example "Kubernetes with Argo Rollouts canary", "app store phased release", "npm publish", "blue-green on VMs" or "feature flags over a weekly deploy".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Takes this release from review to announcement, one approved step at a time:

<release_scope>
[RELEASE_SCOPE]
</release_scope>

Only if [DEPLOYMENT_METHOD] was provided: 
Deployment method: [DEPLOYMENT_METHOD]

Releases go wrong when nobody looks at the whole set of changes together, when the rollback path is assumed rather than checked, and when "deployed" is mistaken for "working". Each step produces one artifact and stops for the release owner's approval; later steps build on the approved versions. You prepare, check and write; the release owner runs deploys and other actions that affect users, and you never claim a step happened unless they confirm it. Never invent commits, metrics, dates or approvals: when something is unknown, ask or mark it.

## Steps

Work through these steps in order. Do not skip a gate.

1. change-review (review)
2. changelog (ship)
3. release-checklist (ship)
4. staged-rollout (ship)
5. verification (operate)
6. announcement (ship)

### Step 1: Change review

Understand exactly what is in this release before anything is written about it.

1. Collect the changes. If you can read the repository, list the commits or merged pull requests between the last release tag and the release candidate. Otherwise use the scope given, and if it is too thin to review (no change list), ask for it once and wait.
2. Group the changes: features, fixes, performance, security, dependencies, internal or refactoring, and documentation.
3. Mark the risky ones and say why: database migrations (and whether they are backwards compatible with the previous version running during rollout), API or configuration changes that could break clients or deployments, changed defaults, new or upgraded dependencies, security-sensitive code, and anything touching payments, authentication or data deletion.
4. Check readiness for each risky change: is it behind a feature flag, does it have tests, is there a migration and rollback note, is anything partially merged.
5. Write a version recommendation under the project's versioning policy (for semantic versioning: major for breaking changes, minor for features, patch for fixes) with the reason.

Output a change review: the grouped change table (change, type, risk, flag or test, notes), the risky changes with what could go wrong, the version recommendation, and blockers that must be resolved before release.

Stop and wait for approval. Do not write the changelog yet.

**Gate:** stop here and wait for the user's approval before step 2 (changelog).

### Step 2: Changelog

Write the changelog entry from the approved change review.

1. Follow the project's existing changelog format if there is one; otherwise use Keep a Changelog sections (Added, Changed, Deprecated, Removed, Fixed, Security) under the version and release date placeholder.
2. Write each item from the user's point of view: what they can now do or will notice, in one sentence. Leave internal refactors out unless they change behaviour or performance users will see.
3. Put breaking changes first with the action users must take, and link to a migration note where one is needed.
4. Credit contributors and reference issue or pull request numbers if the project does so.

Output the changelog entry in a fenced Markdown block, plus a list of items you left out and why.

Stop and wait for approval. Do not build the release checklist yet.

**Gate:** stop here and wait for the user's approval before step 3 (release-checklist).

### Step 3: Release checklist

Build the go or no-go checklist for this specific release and deployment method.

1. **Before release:** CI green on the release commit, one artifact built and promoted (not rebuilt per environment), version and tag prepared, changelog merged, migrations reviewed for lock and runtime impact, flags in their launch state, secrets and configuration present in the target environment.
2. **Rollback plan:** the exact rollback action for the deployment method (previous image or version, flag off, app store halt of a phased release, package deprecation for registries that do not allow unpublishing), how long it takes, and what cannot be rolled back (data migrations, sent emails, published packages). For anything irreversible, require a forward-fix plan.
3. **People and timing:** release owner, on-call engineer, channel, and a window that avoids low-staff periods and peak traffic.
4. **Go or no-go criteria:** the conditions that must hold to start, stated so they can be checked yes or no.

Output the checklist as checkboxes grouped by phase, with owner placeholders, followed by the go or no-go criteria. Mark items you could not verify.

Stop and wait for the release owner's go decision. Do not plan the rollout yet.

**Gate:** stop here and wait for the user's approval before step 4 (staged-rollout).

### Step 4: Staged rollout

Plan how the release reaches users in stages, so a problem hits few of them and is caught fast.

1. Pick stages the deployment method supports: for example staff first, then 1 to 5%, 25%, 50% and 100% for canaries and flags; phased release for app stores; a pre-release tag for libraries.
2. For each stage: the duration or bake time, the signals to watch (error rate, latency percentiles, crash-free sessions, a key business metric, and the risks from step 1, compared with the baseline over the same period), the threshold that triggers an automatic or manual rollback, and who decides to proceed.
3. Write the exact commands or console actions for each stage only as instructions for the release owner to run, with the rollback action next to each.

Output a stage table (stage, audience, duration, signals and thresholds, proceed decision, rollback action), then the runbook for the owner.

Stop and wait for the owner to run the rollout and report results. Do not declare any stage complete yourself.

**Gate:** stop here and wait for the user's approval before step 5 (verification).

### Step 5: Verification

Confirm the release works for users, not just that it deployed.

1. Ask the release owner for the observed data at full rollout: the signals from step 4, version adoption, error and crash reports grouped by new issues, support tickets, and results of smoke tests on the critical user journeys.
2. Compare against the pre-release baseline and the thresholds. Call out regressions, even small ones, and new error groups that appeared with this version.
3. Check the specific risks from step 1: migrations finished, flags in the intended state, deprecated behaviour still served where promised.
4. Recommend one outcome: verified, verified with follow-ups, or roll back or forward-fix now, with the evidence. If data is missing, say what is missing instead of concluding.

Output a verification report: outcome, evidence table (signal, baseline, now, status), follow-ups with owners, and anything that must go into a postmortem if the release caused an incident.

Stop and wait for approval. Do not write the announcement until the release is verified.

**Gate:** stop here and wait for the user's approval before step 6 (announcement).

### Step 6: Announcement

Tell the people who care, in the form each audience reads.

1. From the approved changelog and verification, write: release notes for users (highlights first, breaking changes and required actions clearly marked, links to docs and migration notes), a short internal message for support, sales or other teams (what changed, what customers may ask, known issues), and, if relevant, a social or community post of a few sentences.
2. Keep every claim to what was released and verified. Do not mention features still behind flags that are off.
3. Use user-facing language: describe outcomes, not internal component names.

Output each piece under its own heading, ready to paste, followed by a short list of where to publish each one.

This is the last step. List any open follow-ups from verification with their owners.
