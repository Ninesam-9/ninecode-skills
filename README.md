# NINECODE Skills

Agent Skills for NINECODE: local-first AI workflows for coding agents
(Claude Code, OpenCode). 100% local where possible, no API keys required
unless noted.

## Skills

| Skill | What it does | Needs |
|---|---|---|
| [nine-system](skills/nine-system/SKILL.md) | Diagnose Windows RAM/CPU/disk + Ollama models, recommend which local model/agent fits the task | Ollama + [nine-system-mcp](https://github.com/) (optional; skill also works with plain `ollama` CLI) |

## Install

**Claude Code** (plugin):
```
/plugin marketplace add <tu-usuario>/ninecode-skills
/plugin install ninecode-skills
```

**OpenCode**: copy any `skills/<name>` folder into your skills path
(e.g. `~/.config/opencode/skills/`), or point `skills.paths` at this repo.

## Add a new skill

1. Create `skills/<name>/SKILL.md` with `name:` + `description:` frontmatter.
2. Keep it narrow: one job, trigger phrases in the description, rules over prose.
3. Test it locally, then PR.

## License

MIT - see [LICENSE](LICENSE).
