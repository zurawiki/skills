<img src="assets/icon.png" width="64" alt="">

# Zurawiki Skills

A personal collection of reusable agent skills, packaged as a plugin for Claude Code and Codex.

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

## Layout

- `skills/` holds one `<name>/SKILL.md` per skill.
- `plugin.json` is the portable manifest Codex reads; `.claude-plugin/plugin.json` is the one Claude Code reads. Keep name, version, description, author, and links identical in both.
- `.claude-plugin/marketplace.json` and `.agents/plugins/marketplace.json` list this repo as a one-plugin marketplace for each platform.
