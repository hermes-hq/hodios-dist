---
name: write-shell-script
description: Writes a portable shell script with strict mode, argument parsing, a dry-run flag, clear errors and idempotent steps. Use when automating a chore you will run more than once.
license: CC0-1.0
arguments:
  - goal
  - shell
  - target_os
argument-hint: <goal> [shell] [target_os]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: implementation
  source: https://hermes-ide.com/prompts/write-shell-script
  catalog: 2026.1002.2
---

# Write a robust shell script

## Inputs

- `goal` (required): What the script must do, its inputs, and anything it must never touch.
- `shell` (optional; one of: bash, zsh, posix-sh, powershell; default: bash): Target shell.
- `target_os` (optional; one of: linux, macos, windows, any; default: any): Operating systems the script must run on.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Shell scripts written in a hurry fail in predictable ways: an unset variable expands to an empty string and `rm -rf` hits the wrong directory, a failed command in a pipeline is ignored, a filename with a space splits in two, GNU-only flags break on macOS, and a second run duplicates what the first run did. The person needs a script they can run twice, read in a year, and trust in a dry run first.
</context>

<task>
Write a $shell script for this goal, to run on $target_os:

$goal

1. If the goal leaves out something that decides what gets deleted, overwritten or sent (which paths, which hosts, whether it needs root), ask up to 3 questions and stop. Otherwise state your assumptions and continue.
2. Choose the strict-mode preamble for the shell:
   - bash: `set -Eeuo pipefail`, a `trap` that reports the failing line on ERR, and a cleanup trap on EXIT.
   - zsh: `emulate -L zsh` and `setopt ERR_EXIT NO_UNSET PIPE_FAIL`.
   - posix-sh: `set -eu`. Do not rely on `pipefail`, arrays, `[[ ]]`, `local` or `$'...'`; check pipeline stages explicitly where failure matters.
   - powershell: a `param()` block with `[CmdletBinding(SupportsShouldProcess)]`, `Set-StrictMode -Version Latest` and `$ErrorActionPreference = 'Stop'`; check `$LASTEXITCODE` after native commands.
3. Parse arguments: `-h/--help` (usage to stdout, exit 0), long options, required values validated up front, unknown options rejected with usage on stderr and exit 2. In bash and zsh use a `while`/`case` loop so long options work; `getopts` handles only short ones.
4. Add a dry-run mode (`--dry-run`, or `-WhatIf` in PowerShell) that prints every state-changing command, safely quoted, instead of running it. Route all side effects through one helper so dry run cannot miss one.
5. Make each step idempotent: test before acting, use `mkdir -p` and `ln -sfn`, check before appending to a file, and write files to a temp file on the same filesystem and then move it into place.
6. Fail clearly: check required tools with `command -v` at start-up, print errors to stderr with the script name and a fix, and use distinct non-zero exit codes for distinct failures.
7. Check the script against ShellCheck (or PSScriptAnalyzer) rules in your head, and fix anything they would flag.
</task>

<constraints>
- Quote every expansion. Use `--` before user-supplied paths. Never parse `ls`; use `find ... -print0` with `while IFS= read -r -d ''` (bash/zsh) or a glob loop.
- Guard destructive commands against empty variables with `${VAR:?}`, and never `rm -rf` a path built from unchecked input.
- Portability for macOS and Linux: macOS ships bash 3.2 (no associative arrays, `mapfile` or `${var,,}`) and BSD tools (`sed -i ''`, no `date -d`, no `grep -P`, different `stat` flags). If `target_os` is `any` or `macos`, avoid these or branch on `uname` explicitly.
- No secrets in the script, arguments or logs. Read them from the environment or a file with restricted permissions.
- Never fetch remote code and execute it.
- If the job is better done by an existing tool (rsync, a package manager, a cron entry), say so in one line, then write the script anyway.
</constraints>

<output_format>
## Assumptions
Bullets, or "None".

## Script
One complete code block with a header comment: purpose, usage line, exit codes.

## Usage
Two or three example invocations, including a dry run.

## What it changes
Every file, directory, service or remote system it creates, modifies or deletes.

## How to test it
Steps to try it safely: dry run first, then a throwaway directory or container.

## Limitations
What it does not handle, one line each.
</output_format>
