# hodios-dist

**Hodios — prompts by Hermes IDE.** This repository is the generated install tree: Agent Skills, plugins and marketplaces, written only by the release bot.

**Do not open pull requests here.** The source, issues and discussions live in [hermes-hq/hodios](https://github.com/hermes-hq/hodios). Browse the library at [hermes-ide.com/prompts](https://hermes-ide.com/prompts).

The first catalog release has not shipped yet. When it does, this repository will hold:

- `skills/<id>/SKILL.md` for `npx skills add hermes-hq/hodios-dist`, `gh skill install` and `gemini skills install`
- `.claude-plugin/marketplace.json` and `plugins/` for `claude plugin marketplace add hermes-hq/hodios-dist` and the Copilot CLI
- drop-in trees for other tools under `native/`, and paste-ready text under `paste/`

Content is dedicated to the public domain under [CC0-1.0](LICENSE).
