# Claude Code Helpers

This directory contains helper files and ways of working for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Files

| File | Description |
|------|-------------|
| [CLAUDE.md](./CLAUDE.md) | Agent instructions, ways of working, and Claude Code-specific reminders |

## Native paths

| Scope | Path | Notes |
|-------|------|-------|
| Global | `~/.claude/CLAUDE.md` | Applies to every Claude Code session on this machine |
| Project | `<repo-root>/CLAUDE.md` | Checked into version control; shared with the team |
| Local override | `<repo-root>/CLAUDE.local.md` | Gitignored; personal preferences not shared with the team |

Claude Code merges all three layers. Project-level instructions override global ones; local overrides win over both.

## Quickstart

Copy `CLAUDE.md` into the root of your project:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/claude-code/CLAUDE.md \
  -o CLAUDE.md
```

For a global baseline (applies to all your projects), install it to the Claude Code global path:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/claude-code/CLAUDE.md \
  -o ~/.claude/CLAUDE.md
```
