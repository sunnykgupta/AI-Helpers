# Codex Helpers

This directory contains helper files and ways of working for [OpenAI Codex](https://openai.com/codex).

## Files

| File | Description |
|------|-------------|
| [AGENTS.md](./AGENTS.md) | Agent instructions and ways of working for Codex |

## Native paths

| Scope | Path | Notes |
|-------|------|-------|
| Global | `~/.codex/AGENTS.md` | Applies to every Codex session on this machine |
| Repo root | `<repo-root>/AGENTS.md` | Checked into version control; shared with the team |
| Subdirectory | `<dir>/AGENTS.md` | Scoped to tasks within that directory |
| Override | `<repo-root>/AGENTS.override.md` | Gitignored; local overrides merged on top |

Codex merges these layers in order (global → repo → subdirectory → override). Each layer adds to or selectively overrides the previous one.

## Quickstart

Copy `AGENTS.md` into the root of your project:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/codex/AGENTS.md \
  -o AGENTS.md
```

For a global baseline (applies to all your projects), install it to the Codex global path:

```bash
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/codex/AGENTS.md \
  -o ~/.codex/AGENTS.md
```
