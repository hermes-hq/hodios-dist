---
name: containerize-app-track
description: Containerises an existing app in gated steps, detecting the stack, writing a multi-stage Dockerfile and compose file, then building, running and documenting it. Use when an app has no containers yet.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: devops
  source: https://hermes-ide.com/prompts/containerize-app-track
  catalog: 2026.1004.1
---

# Containerise an existing app

## Inputs

- [APP_PATH] (required): Path to the app inside the repository, for example "." or "services/api".
- [SERVICES] (optional): Backing services the app needs locally, such as "PostgreSQL 16, Redis". Leave empty and step 1 detects them from config and code.
- [TARGET] (optional; one of: local-dev, production, both; default: local-dev): What the images are for. local-dev adds hot reload and dev tools; production builds a lean, locked-down image; both builds separate targets from one Dockerfile.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Puts the app at `[APP_PATH]` into containers that build reproducibly and actually start, for [TARGET] use. The common failures are a Dockerfile that copies the whole repo before installing dependencies (slow, cache-busting builds), runs as root, bakes secrets or `.env` files into a layer, ignores the lockfile, or has no health check, so compose starts the app before its database is ready. This track detects how the app really builds and runs, writes the files, proves them with a local build and run, and documents them.

Rules for every step:
- Derive commands, ports, versions and environment variables from the repository (manifests, scripts, config, CI). Ask instead of guessing when something cannot be found.
- Never copy secrets, `.env` files, credentials or private keys into an image. Use build secrets for private package registries and runtime environment variables for configuration, with an example env file holding placeholders only.
- Do not push images, log in to registries or deploy anything.
- Follow the repo's existing conventions if container files already exist; improve them rather than adding parallel ones, and say what changed.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.

## Steps

Work through these steps in order. Do not skip a gate.

1. detect (discover)
2. dockerfile (build)
3. compose (build)
4. run-and-document (verify)

### Step 1: Detect how the app builds and runs

<services>
[SERVICES]
</services>

1. Identify the language, runtime version (from version files and manifests), package manager and lockfile, build command, start command for production and for development, and the port it listens on.
2. List the environment variables the app reads (config modules, `.env.example`, framework settings) and which are secrets.
3. Find backing services from the services list above, config, connection strings and dependencies (database drivers, cache and queue clients). Note versions where config or CI pins them.
4. Note runtime needs: files it writes (uploads, caches, logs: should go to stdout), background workers or schedulers that need their own container, migrations and how they run, assets compiled at build time, system libraries native dependencies need, and a health or readiness endpoint (or where one could be added).
5. Check for existing Dockerfiles, compose files, `.dockerignore` and devcontainer config.

Write the artifact: Stack, Commands, Environment (Variable | Secret | Default | Source), Services, Runtime needs, Existing container files, Plan for [TARGET], Open questions. Stop and wait for approval.

Save this step's result to `containerize/01-detect.md`.

**Gate:** stop here and wait for the user's approval before step 2 (dockerfile).

### Step 2: Write the Dockerfile and .dockerignore

1. Multi-stage build: a dependencies stage that copies only manifests and lockfile and installs with the locked, reproducible command (for example `npm ci`, `pip install --require-hashes` or a lockfile-aware tool, `bundle install` with `BUNDLE_DEPLOYMENT=1` and `BUNDLE_FROZEN=1`, `go mod download`); a build stage; and a runtime stage that copies only what runs.
2. Base images: an official image pinned to a specific version tag matching the detected runtime, in the variant the app's native dependencies support. Note that pinning by digest is stronger and how to update it.
3. Runtime stage: a non-root user, a working directory, the port documented with `EXPOSE`, exec-form `CMD` or `ENTRYPOINT` so signals reach the process (with an init process if the app spawns children), and a `HEALTHCHECK` against the health endpoint or a cheap command.
4. For local-dev or both: a dev target with dev dependencies and a start command that supports hot reload through a bind mount; keep it separate from the production target.
5. `.dockerignore`: version control folders, local env files, dependency folders, build output, test artefacts, editor files, and anything secret.
6. Order layers so code changes do not invalidate the dependency install.

Continue to step 3.

### Step 3: Write the compose file

1. One service for the app (built from the right target) and one per backing service from step 1, using official images pinned to the versions found.
2. Health checks for every service, and `depends_on` with `condition: service_healthy` so the app starts only when its dependencies are ready. Run migrations as a one-off service or an entrypoint step that the app waits on, matching how the project runs them.
3. Named volumes for database data; bind mounts for source code only in the dev setup.
4. Configuration through an env file referenced by compose, with a committed example file holding placeholders and a git-ignored real one.
5. Expose only the ports a developer needs on the host.

Continue to step 4.

### Step 4: Build, run, verify and document

1. Build every target. Record build time, a rebuild time after a code-only change (to prove layer caching works), and the final image size.
2. Start the stack with compose and wait until every service reports healthy. Call the health endpoint and one real endpoint or command. Run the test suite inside the container if the project's tests can run there.
3. Confirm the runtime container runs as a non-root user, contains no `.env` file or secret (inspect the image filesystem and history), and stops cleanly on a stop signal within the timeout.
4. Tear the stack down, removing volumes created for the test.
5. Add usage docs where the project keeps them (README section or a short doc): prerequisites, first run, everyday commands, how to reset data, how to run tests and migrations, and the environment variables.

Write the report:

#### Files
One line per file added or changed.

#### Verification
Each check above with its real result: build, rebuild, size, health, endpoint, tests, user, secrets, shutdown.

#### Usage
The commands a developer needs, as documented.

#### Not done
Production concerns outside this track, such as registry, image signing, orchestration manifests and scanning, as one-line follow-ups.

Save this step's result to `containerize/04-report.md`.
