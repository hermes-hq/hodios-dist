# hodios-dist

**Hodios — prompts by Hermes IDE.** This repository is the generated install tree for catalog `2026.1004.1`: 1,996 entries (the curated tier, of 3,601 in the catalog) compiled into Agent Skills, Claude Code plugins and drop-in files for each tool. It is written only by the release bot.

The installers below download this whole repository, so it holds the curated tier only, at most 2,000 entries. Every other entry is in `catalog/v1/` and installs with the `hodios` CLI: `npx @hermes-hq/hodios search <words>`, then `npx @hermes-hq/hodios install <id> --target claude-code`.

**Do not open pull requests here.** The source, issues and discussions live in [hermes-hq/hodios](https://github.com/hermes-hq/hodios).

## Install

| Tool | Command |
|---|---|
| Claude Code | `claude plugin marketplace add hermes-hq/hodios-dist` then `claude plugin install hodios-software-engineering@hodios` |
| Any agent that reads Agent Skills | `npx skills add hermes-hq/hodios-dist --skill review-pull-request` |
| Gemini CLI | `gemini skills install https://github.com/hermes-hq/hodios-dist --path skills/review-pull-request --consent` |
| Any entry, curated or not | `npx @hermes-hq/hodios install <id> --target claude-code` (or `codex`, `cursor`, `copilot`, `gemini-cli`, `opencode`, `agents-md`) |

Each Claude Code plugin is one domain, named `hodios-<domain>` (for example `hodios-software-engineering`, `hodios-education`, `hodios-travel`). `claude plugin marketplace list` and `/plugin` show them all.

## Layout

| Path | What it holds |
|---|---|
| `.claude-plugin/marketplace.json` | The Claude Code marketplace, one plugin per domain |
| `plugins/hodios-<domain>/` | Claude Code plugins: skills, subagents and output styles |
| `skills/<id>/SKILL.md` | One Agent Skill per curated entry, plus `agents/openai.yaml` for Codex |
| `native/<tool>/` | Project trees to copy into a repo: `claude-code`, `codex`, `cursor`, `copilot`, `gemini-cli`, `opencode`, `agents-md` |
| `paste/<id>.md` | Paste-in text for ChatGPT, claude.ai and any chat tool, per curated entry |
| `bundles/all.hermes-prompts` | The curated tier for Hermes IDE |
| `catalog/v1/` | The searchable catalog the `hodios` CLI reads, with every entry in every tier: `manifest.json` plus content-addressed objects under `o/` |

Rules (always-on project instructions) are not in the Claude Code plugins, because plugins cannot carry them. Copy them from `native/<tool>/` instead.

Content is dedicated to the public domain under [CC0-1.0](LICENSE).
