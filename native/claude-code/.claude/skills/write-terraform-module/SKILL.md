---
name: write-terraform-module
description: Writes a reusable Terraform module with typed, validated variables, secure defaults, documented outputs and an example. Use when wrapping cloud resources for other teams to consume.
license: CC0-1.0
arguments:
  - resource_goal
  - cloud
  - constraints
argument-hint: <resource_goal> [cloud] [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: devops
  source: https://hermes-ide.com/prompts/write-terraform-module
  catalog: 2026.1004.3
---

# Write a Terraform module

## Inputs

- `resource_goal` (required): What the module should provision and for whom, e.g. "private S3 bucket for app uploads with lifecycle rules".
- `cloud` (optional; one of: aws, gcp, azure, cloudflare; default: aws): Target provider.
- `constraints` (optional): Org rules to honour, such as naming, tagging, regions, compliance or provider versions.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A Terraform module is an API. Its variables are the inputs other teams depend on and its outputs are the contract they build on, so changing either later is a breaking change. Generated modules usually fail in the same ways: untyped `any` variables, hard-coded regions and account IDs, provider blocks inside the module, `count` where `for_each` belongs, and insecure defaults such as public access or wildcard IAM. The target here is a module a platform team would publish to its internal registry.
</context>

<task>
Write a reusable Terraform module for $cloud that does this:
$resource_goal
Only if constraints was provided: 
Honour these constraints:
$constraints

1. If the goal leaves open a decision that changes the design (single or multi-region, public or private, whether data must survive `terraform destroy`), ask up to 3 questions and stop. If the gap is a detail, choose the safe default and record it under Assumptions.
2. Draw the boundary: one cohesive purpose. Take shared things (VPC or network IDs, KMS keys, DNS zones) as inputs instead of creating them.
3. Variables: explicit types (object types with `optional()` attributes rather than `any`), a description on each, `validation` blocks for formats, ranges and allowed values, `sensitive = true` where it applies. Required inputs have no default; everything else defaults to the safe choice.
4. Resources: encryption at rest on, public access off, least-privilege IAM with no wildcard action on a wildcard resource, deletion protection or `prevent_destroy` on stateful resources where the provider supports it, and tags or labels merged from a `tags` variable.
5. Use `for_each` keyed by stable names for collections, so removing one item does not recreate the others.
6. Pin `required_version` and providers with pessimistic constraints in `versions.tf`. Never put a `provider` or `backend` block in the module itself; only the example under `examples/` configures a provider, because it is a root module.
7. Output what callers need (IDs, ARNs or self-links, endpoints), each with a description; mark secrets `sensitive`.
</task>

<constraints>
- Use only resources and arguments that exist in the current $cloud provider. If you are unsure an argument exists in the pinned version, say so under Assumptions instead of guessing silently.
- No hard-coded account IDs, regions, CIDRs, image IDs or names. They come from variables or data sources.
- No provisioners or `local-exec` unless the goal cannot be met otherwise; explain why if you use one.
- The code must pass `terraform fmt` and `terraform validate`. You cannot run them here, so do not claim they pass.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Assumptions
Bullets: each default you chose and why. "None" if the goal settled everything.
## Files
One fenced `hcl` block per file, headed by its path: `versions.tf`, `variables.tf`, `main.tf`, `outputs.tf`, `examples/basic/main.tf`.
## README
An inputs table (name, type, default, description), an outputs table, and a short usage paragraph.
## Verify
The commands to run (`terraform fmt -check`, `terraform validate`, `terraform plan` on the example, plus a static scanner such as tflint or checkov) and what to look for in the plan.
</output_format>
