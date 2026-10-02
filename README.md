# hodios-dist

**Hodios — prompts by Hermes IDE.** This repository is the generated install tree for catalog `2026.1002.0`: 203 entries compiled into Agent Skills, Claude Code plugins and drop-in files for each tool. It is written only by the release bot.

**Do not open pull requests here.** The source, issues and discussions live in [hermes-hq/hodios](https://github.com/hermes-hq/hodios).

## Install

| Tool | Command |
|---|---|
| Claude Code | `claude plugin marketplace add hermes-hq/hodios-dist` then `claude plugin install hodios-code-review@hodios` |
| Any agent that reads Agent Skills | `npx skills add hermes-hq/hodios-dist --skill review-pull-request` |
| Gemini CLI | `gemini skills install https://github.com/hermes-hq/hodios-dist --path skills/review-pull-request --consent` |

Each Claude Code plugin is one category, named `hodios-<category>` (for example `hodios-testing`, `hodios-security`, `hodios-debugging`). `claude plugin marketplace list` and `/plugin` show them all.

## Layout

| Path | What it holds |
|---|---|
| `.claude-plugin/marketplace.json` | The Claude Code marketplace, one plugin per category |
| `plugins/hodios-<category>/` | Claude Code plugins: skills, subagents and output styles |
| `skills/<id>/SKILL.md` | One Agent Skill per entry, plus `agents/openai.yaml` for Codex |
| `native/<tool>/` | Project trees to copy into a repo: `claude-code`, `codex`, `cursor`, `copilot`, `gemini-cli`, `opencode`, `agents-md` |
| `paste/<id>.md` | Paste-in text for ChatGPT, claude.ai and any chat tool |
| `bundles/all.hermes-prompts` | The whole catalog for Hermes IDE |

Rules (always-on project instructions) are not in the Claude Code plugins, because plugins cannot carry them. Copy them from `native/<tool>/` instead.

Content is dedicated to the public domain under [CC0-1.0](LICENSE).
