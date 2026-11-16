<img src="assets/icon.png" width="64" alt="">

# zurawiki/skills

A personal collection of reusable agent skills, packaged as a plugin for Claude Code, Codex, and Cursor.

## Skills

| Skill | Use it when |
| :- | :- |
| `principle-fix-root-causes` | Debugging: trace each symptom to the first place the system went wrong and fix it there. |
| `principle-laziness-protocol` | Refactoring or weighing diff size: bias toward deletion and the smallest change that solves the problem. |
| `principle-subtract-before-you-add` | Sequencing an addition, refactor, or rewrite: remove dead code first, then build on the simpler base. |

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

Cursor: the repo is a Cursor plugin (`.cursor-plugin/plugin.json`); add it by its GitHub URL.

## Layout

- `skills/` holds one `<name>/SKILL.md` per skill.
- `plugin.json` is the portable manifest Codex reads; `.claude-plugin/plugin.json` and `.cursor-plugin/plugin.json` are the ones Claude Code and Cursor read. Keep name, version, description, author, license, and links identical in all three.
- `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json` list this repo as a one-plugin marketplace for Claude Code and Codex.

## License

MIT
