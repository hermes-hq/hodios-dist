---
name: review-cloud-iam-policy
description: Reviews AWS, GCP or Azure IAM policies for over-broad permissions, privilege-escalation paths, wildcard resources and missing conditions, and proposes least-privilege versions.
license: CC0-1.0
arguments:
  - policies
  - cloud
  - intended_use
argument-hint: <policies> <cloud> [intended_use]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: security
  source: https://hermes-ide.com/prompts/review-cloud-iam-policy
  catalog: 2026.1002.2
---

# Review a cloud IAM policy

## Inputs

- `policies` (required): The policies as JSON, YAML, Terraform or CLI output - identity policies, role bindings, trust or assume-role policies, resource policies and custom role definitions.
- `cloud` (required; one of: aws, gcp, azure): Which cloud the policies belong to.
- `intended_use` (optional): Who or what uses this identity and what it must be able to do (for example "CI deploys one Lambda function and reads one S3 bucket").

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Cloud breaches rarely need an exploit; they use permissions that were granted too broadly. The dangerous grants are not always the obvious wildcards. A narrow-looking permission can let an identity give itself more: passing a privileged role to a compute service it controls, impersonating a service account, editing its own policy, or creating credentials for a more powerful identity. Trust policies and resource policies can open access to whole accounts, organisations or the public. A useful review reads every statement with its conditions, follows each escalation path to its end, and checks the grant against what the identity actually needs.
</context>

<task>
Review these $cloud IAM policies:

<policies>
$policies
</policies>
Only if intended_use was provided: 

Intended use: $intended_use

1. Summarise what the identity can effectively do, statement by statement or binding by binding, including inherited scope (organisation, folder, management group, subscription, account) and any deny statements, boundaries or conditions that limit it.
2. Flag over-broad grants: wildcard actions or services, wildcard or account-wide resources, `NotAction` or `NotResource` combined with `Allow`, broad built-in roles (AWS managed admin policies; GCP basic roles Owner, Editor and Viewer; Azure Owner, Contributor and User Access Administrator) where a narrower role exists, and grants at a higher scope than needed.
3. Trace privilege-escalation paths specific to $cloud, for example:
   - AWS: `iam:PassRole` on broad resources combined with the ability to create or update compute (Lambda, EC2, ECS, Glue, CloudFormation); `iam:CreatePolicyVersion`, `iam:SetDefaultPolicyVersion`, `iam:Put*Policy`, `iam:Attach*Policy`, `iam:UpdateAssumeRolePolicy`, `iam:CreateAccessKey` or `iam:CreateLoginProfile` on other principals; `sts:AssumeRole` on `*`; `ssm:SendCommand` to privileged instances.
   - GCP: `iam.serviceAccounts.actAs`, `getAccessToken`, `signBlob` or `implicitDelegation` on privileged service accounts; Service Account Token Creator or Key Admin roles; `setIamPolicy` on projects, folders or service accounts; deploying compute that runs as a privileged service account.
   - Azure: `Microsoft.Authorization/roleAssignments/write` or `roleDefinitions/write`; custom roles with `*` actions; managed identities with high roles attached to resources the identity can modify; Entra ID roles or app permissions that can add credentials to privileged applications or assign directory roles.
   For each path: the starting permission, the steps and the end privilege.
4. Check trust and resource policies: principals of `*`, whole accounts or all authenticated users without conditions; public access (`allUsers`, anonymous blob access, public bucket policies); third-party role trust without an external id; and federated identity trust (CI OIDC providers, workload identity federation) without conditions pinning the repository, branch or audience.
5. Check missing conditions that would narrow risky grants: organisation membership, source account or ARN for service principals (confused deputy), network or VPC restrictions, MFA for human access, tag-based scoping, time-bound access.
6. Compare against the intended use and write a least-privilege version: specific actions, specific resources, conditions, and separate identities where one identity serves unrelated purposes. If the intended use is not given, infer it from the policy, label the inference, and ask the owner to confirm before tightening.
7. Say how to verify before applying: the cloud's own policy analysis and last-used or recommender data, and a test of the real workload in a non-production environment.
</task>

<constraints>
- Use the exact permission and role names for $cloud; do not mix clouds.
- Every finding names the statement or binding, the risk, a concrete misuse and the fix. If a statement is safe because of a condition or boundary, say so instead of flagging it.
- Rank by impact: account or organisation takeover and data exposure before hygiene.
- Do not tighten a policy in a way that breaks the stated use; when unsure whether a permission is needed, mark it "verify with access logs" rather than removing it silently.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: approve | approve with changes | reject. Then the highest risk in one sentence.

## Findings
Numbered, most severe first. Each: severity (critical, high, medium, low) - statement or binding - what is wrong - how it could be misused - fix.

## Escalation paths
For each path: start permission, then each step, then the end privilege. "None found" if none.

## Least-privilege version
The rewritten policies in the same format as the input, in code blocks, with comments where a permission needs confirmation.

## Verify before applying
Numbered checks with the tool or log to use.
</output_format>
