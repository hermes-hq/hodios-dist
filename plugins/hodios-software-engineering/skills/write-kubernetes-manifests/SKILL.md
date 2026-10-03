---
name: write-kubernetes-manifests
description: Writes production-ready Kubernetes manifests for a service with probes, resource requests, a disruption budget and a restricted security context. Use when deploying a service to a cluster.
license: CC0-1.0
arguments:
  - service
  - environment
  - packaging
argument-hint: <service> [environment] [packaging]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: devops
  source: https://hermes-ide.com/prompts/write-kubernetes-manifests
  catalog: 2026.1003.2
---

# Write Kubernetes manifests

## Inputs

- `service` (required): The service to deploy - image, ports, protocol, dependencies, config and secrets it reads, expected traffic, statefulness.
- `environment` (optional; one of: dev, staging, prod; default: prod): Environment the manifests target; sets replica counts, budgets and sizing.
- `packaging` (optional; one of: plain, kustomize, helm; default: plain): How to package the output.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most Kubernetes outages caused by manifests come from a short list: liveness probes that check a database and restart every pod when it blips, no readiness probe so traffic hits pods that are still starting, missing memory requests so the scheduler overpacks nodes, a disruption budget that blocks every node drain, all replicas on one node or zone, and containers running as root with a writable filesystem. These manifests should survive a node drain, a zone loss and a security review.
</context>

<task>
Write Kubernetes manifests for this service, for the $environment environment, packaged as $packaging:
$service

1. If the description lacks the image, the listening port or whether the service holds state, ask for them and stop. Everything else you may default; record each default under Assumptions.
2. A stateless service gets a Deployment; one that owns disk state gets a StatefulSet. Say which and why.
3. Deployment: rolling update with `maxUnavailable: 0` and a small `maxSurge`; replicas of at least 3 in prod, 2 in staging, 1 in dev; topology spread constraints across zones and nodes; a dedicated ServiceAccount with `automountServiceAccountToken: false` unless the app calls the API server.
4. Probes with distinct jobs: a startup probe for slow boots, a readiness probe that reflects ability to serve, and a liveness probe that checks only the process itself, never downstream dependencies.
5. Resources: CPU and memory requests sized from the description; a memory limit equal to the memory request; no CPU limit unless the user asks for one (explain the throttling trade-off).
6. Security context: `runAsNonRoot`, a numeric non-zero UID, `readOnlyRootFilesystem` (with an `emptyDir` for any scratch path), `allowPrivilegeEscalation: false`, all capabilities dropped, `seccompProfile: RuntimeDefault`. Label the namespace for the `restricted` Pod Security Standard.
7. Graceful shutdown: a `terminationGracePeriodSeconds` and a short `preStop` sleep so endpoints are removed before the process stops.
8. Also write: a Service, a PodDisruptionBudget (`maxUnavailable: 1`; omit it when replicas are 1, because it would block drains), a HorizontalPodAutoscaler for prod, and a NetworkPolicy that denies ingress except from the callers described.
9. Config comes from a ConfigMap; secrets are referenced by name from a Secret or external secret store, never written with values.
10. Packaging: `plain` is one multi-document YAML file; `kustomize` is a base plus an overlay per environment; `helm` is a chart with `values.yaml`, templates and per-environment values files.
</task>

<constraints>
- Use stable API versions only (`apps/v1`, `policy/v1`, `autoscaling/v2`, `networking.k8s.io/v1`).
- Pin the image by digest or an immutable version tag, never `latest`.
- Do not invent hostnames, registry paths or secret names; use clearly marked placeholders such as `REPLACE_ME_REGISTRY` and list them under Assumptions.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Assumptions
Bullets: every default and placeholder.
## Manifests
One fenced `yaml` block per file, headed by its path.
## Why these values
A table: setting, value, reason. Cover replicas, probes, requests and limits, the disruption budget and the security context.
## Verify
Commands: `kubectl apply --dry-run=server`, a schema check such as kubeconform, and how to confirm the rollout and a node drain behave as intended.
</output_format>
