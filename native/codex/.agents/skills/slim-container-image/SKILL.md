---
name: slim-container-image
description: Rewrites a Dockerfile for a smaller, faster, safer image with multi-stage builds, cache-friendly layers, pinned bases and a non-root user. Use when images are large, slow or flagged by scanners.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: devops
  source: https://hermes-ide.com/prompts/slim-container-image
  catalog: 2026.1002.2
---

# Slim down a container image

## Inputs

- [DOCKERFILE] (required): The current Dockerfile, plus the lockfile names and build command if they are not obvious from it.
- [RUNTIME] (optional): Language runtime and version, e.g. "node 22", "python 3.12 with numpy", "go 1.23", "java 21 spring boot".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Image size, build time and attack surface usually come from the same mistakes: compilers and dev dependencies shipped to production, source copied before dependencies so every code change reinstalls everything, floating base tags, package-manager caches left in layers, secrets passed as build args, and a root user. A good rewrite fixes all of these without changing how the application behaves at runtime.
</context>

<task>
Rewrite this DockerfileOnly if [RUNTIME] was provided:  for [RUNTIME]:
[DOCKERFILE]

1. Work out the runtime, the package manager and the build output from the file. If you cannot tell the runtime or what command starts the app, ask and stop.
2. Split into stages: a build stage with the toolchain, and a runtime stage with only what runs. Choose the runtime base deliberately: distroless or a `-slim` image by default; `scratch` only for static binaries; Alpine only if you have checked that musl will not break native modules or Python wheels, and say so.
3. Order layers for caching: copy lockfiles, install dependencies, then copy source. Use BuildKit cache mounts for package caches, install production dependencies only in the final stage, and clean package lists in the same `RUN` that creates them.
4. Pin each base image by tag plus digest (leave the digest as a placeholder for the user to fill if you do not know it).
5. Run as a non-root user with a numeric UID and GID; make application files owned by root and read-only unless the app must write to them.
6. Replace any secret passed through `ARG` or `ENV` with a BuildKit secret mount.
7. Use exec-form `ENTRYPOINT`/`CMD` and make sure the process receives signals (an init such as tini when the runtime does not reap children).
8. Write a `.dockerignore` that excludes VCS data, local env files, tests and build caches.
</task>

<constraints>
- Keep runtime behaviour the same: exposed port, entrypoint semantics, working directory, environment variables and file paths the app reads. List anything you had to change under "Behaviour to check".
- Size and time savings are estimates unless you were given measurements. Label them as estimates.
- Do not add tools the original image did not need (curl, shells) "for debugging".
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Dockerfile
The full rewritten file in one fenced block, with short comments only where a choice is non-obvious.
## .dockerignore
One fenced block.
## Changes
A table: change, why, effect on size, build time or security.
## Behaviour to check
Bullets, or "None".
## Verify
Commands to compare image size and layers before and after, run the container as a non-root user, and scan it.
</output_format>
