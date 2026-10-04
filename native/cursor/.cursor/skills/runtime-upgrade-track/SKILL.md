---
name: runtime-upgrade-track
description: Upgrades a language runtime across code, lockfiles, Docker images, CI and docs, fixing deprecations and running the full suite at each gate. Use before a runtime version reaches end of life.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: migration
  source: https://hermes-ide.com/prompts/runtime-upgrade-track
  catalog: 2026.1004.3
---

# Upgrade a project's language runtime

## Inputs

- [RUNTIME] (optional; one of: node, python, java, dotnet, ruby, go; default: node): The runtime being upgraded.
- [TARGET_VERSION] (required): The version to move to, for example "22", "3.13", "21", "9.0", "3.4" or "1.23".
- [TEST_COMMAND] (required): The command that runs the full test suite.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Moves this project to [RUNTIME] [TARGET_VERSION] everywhere it runs, not just on one laptop. A runtime upgrade usually fails in the places nobody looks: a CI matrix still on the old version, a Docker base image, a serverless runtime setting, a native module without a build for the new version, or a deprecation that only warns at runtime. This track finds every pin first, reads the official release notes for each version crossed, upgrades in one consistent change, and proves it with the full suite.

Rules for every step:
- Use the official release notes and migration guides for every version between the current one and [TARGET_VERSION]. Cite them for each breaking change you act on. Do not rely on memory for what changed.
- Upgrade dependencies only when the new runtime needs it, one reason per dependency, and keep them out of the change otherwise.
- Every claim of "passes" comes from a real run of `[TEST_COMMAND]` or a real build on the target version.
- Do not deploy, push images or change shared infrastructure. Prepare the changes and say what someone must roll out.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.

## Steps

Work through these steps in order. Do not skip a gate.

1. inventory (discover)
2. upgrade (build)
3. verify (verify)

### Step 1: Find every pin and every breaking change

1. Confirm the current version and that [TARGET_VERSION] is a released, supported version of [RUNTIME] (check the official release schedule). If it is not, say so and stop.
2. Find every place the version is pinned or assumed. Search for all of these that apply:
   - Version files: `.nvmrc`, `.node-version`, `.python-version`, `.ruby-version`, `.tool-versions`, `.sdkmanrc`, `global.json`, `rust-toolchain`-style files.
   - Manifests: `engines` in package.json, `requires-python` and classifiers in pyproject or setup files, `ruby` in the Gemfile, `go` and `toolchain` directives in go.mod, Maven or Gradle toolchain and release level, `TargetFramework` in project files.
   - Images and environments: Dockerfile `FROM` lines, compose files, devcontainer config, CI matrices and setup actions, serverless and platform runtime settings, Helm values and infrastructure code.
   - Docs: README, CONTRIBUTING, onboarding notes.
3. Read the release notes and migration guides for each version crossed and list the breaking changes and removals that could touch this code. Search the code for each one.
4. Check dependencies: packages with native extensions or engine constraints, minimum versions known to support the target, and any dependency pinned to the old runtime.
5. Run `[TEST_COMMAND]` on the current version to record the baseline, including deprecation warnings.

Write the artifact: Baseline, Pins (File | Current | Change), Breaking changes (Change | Source | Where it hits | Fix), Dependencies to bump (Package | From | To | Why), Risks. Stop and wait for approval.

Save this step's result to `runtime-upgrade/01-inventory.md`.

**Gate:** stop here and wait for the user's approval before step 2 (upgrade).

### Step 2: Upgrade in one consistent change

1. Install [RUNTIME] [TARGET_VERSION] locally with the project's version manager, without changing the system default.
2. Update every approved pin to the same version. Keep major-only pins where the project uses them, and match the base image variant (slim, alpine, distroless) already in use.
3. Bump the approved dependencies and regenerate the lockfile with the target version, so resolution reflects it. Do not upgrade unrelated packages.
4. Fix the breaking changes from step 1 in the code, one kind at a time.
5. Turn deprecation warnings into visible output for the test run (for example `--trace-deprecation` or `NODE_OPTIONS` for Node, `-W error::DeprecationWarning` for a check run in Python, `-Xlint:deprecation` for Java, `RUBYOPT=-W:deprecated` for Ruby, analyzers for .NET, `go vet` for Go) and fix the ones introduced by the target version.
6. Run `[TEST_COMMAND]` after each kind of fix.

Continue to step 3.

### Step 3: Verify everywhere and report

1. Run `[TEST_COMMAND]` in full on [TARGET_VERSION]. Compare with the baseline: no new failures, no new skips.
2. Build the production artifact and any Docker image, and run the app or a smoke command inside it to prove the image starts on the new runtime.
3. Run the linters, type checker and build that CI runs. Validate that every CI file you changed is syntactically valid.
4. Confirm no pin was missed: search the repo again for the old version string.

Write the report:

#### Result
Commands run on the target version and their real results, compared with the baseline.

#### Pins changed
One line per file.

#### Code changes
Each breaking change fixed, with its source.

#### Dependencies bumped
Package, from, to, why.

#### Rollout notes
What must change outside the repo (platform runtime settings, base images in other repos, developer machines) and in what order.

#### Left open
Deprecations deferred, warnings remaining, anything not verified.

Save this step's result to `runtime-upgrade/03-report.md`.
