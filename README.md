<img src="assets/icon.png" width="64" alt="">

# zurawiki/skills

A personal collection of reusable agent skills, packaged as a plugin for Claude Code, Codex, and Cursor.

## Skills

Browse the [skills directory](skills/). To add a skill, create `skills/<name>/SKILL.md` with its name, description, and instructions.

## Install

Claude Code:

```bash
claude plugin marketplace add zurawiki/skills
claude plugin install skills@zurawiki
```

Codex:

```bash
codex plugin marketplace add zurawiki/skills
codex plugin add skills@zurawiki
```

In Cursor, add this repository by its GitHub URL.

## Layout

- `plugin.json` configures Codex. Claude Code reads `.claude-plugin/plugin.json` and Cursor reads `.cursor-plugin/plugin.json`. Keep name, version, description, author, license, and links identical in all three.
- `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json` list this repo as a one-plugin marketplace for Claude Code and Codex.

## License

MIT
