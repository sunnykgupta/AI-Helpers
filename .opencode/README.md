# OpenCode Helpers

This directory contains helper files and ways of working for [OpenCode](https://opencode.ai).

## Files

| File | Description |
|------|-------------|
| [AGENTS.md](./AGENTS.md) | Agent instructions, ways of working, and OpenCode-specific reminders |
| [..opencode/skills/](./..opencode/skills/) | Reusable skill definitions (PR descriptions, commit messages, code review) |
| [..opencode/agents/](./..opencode/agents/) | Custom agent configurations (code-reviewer, review-runner) |
| [..opencode/rules/](./..opencode/rules/) | Language-scoped rules (TypeScript, Python) |

## Native paths

| Scope | Path | Notes |
|-------|------|-------|
| Global | `~/.config/opencode/AGENTS.md` | Applies to every OpenCode session on this machine |
| Project | `<repo-root>/AGENTS.md` | Checked into version control; shared with the team |
| Global skills | `~/.config/opencode/skills/<name>/SKILL.md` | Available globally |
| Project skills | `.opencode/skills/<name>/SKILL.md` | Scoped to this project |
| Global agents | `~/.config/opencode/agents/<name>.md` | Available globally |
| Project agents | `.opencode/agents/<name>.md` | Scoped to this project |
| Project rules | `.opencode/rules/<name>.md` | Additional instruction files |

OpenCode also reads `CLAUDE.md` as a fallback if `AGENTS.md` doesn't exist, and `.claude/skills/` for Claude Code compatibility.

## Quickstart

Copy `AGENTS.md` into the root of your project:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/AGENTS.md \
  -o AGENTS.md
```

For a global baseline (applies to all your projects), install it to the OpenCode global path:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/AGENTS.md \
  -o ~/.config/opencode/AGENTS.md
```

## Skills

OpenCode should consult the skills in `..opencode/skills/` for the following tasks:

- **Writing commit messages** → use the `commit-message` skill
- **Writing PR descriptions** → use the `pr-description` skill
- **Code review** → use the `codereview` skill

## Custom Agents

OpenCode comes with built-in agents (build, plan, general, explore). You can also define custom agents in `..opencode/agents/`:

- **code-reviewer** — Read-only code review (no file edits)
- **review-runner** — Full code review that runs linting, typechecks, and tests

## Rules

Additional instruction files can be referenced in `AGENTS.md` using the `@` syntax, or via the `instructions` field in `opencode.json`.