# Cursor Helpers

This directory contains helper files and ways of working for [Cursor](https://www.cursor.com/).

## Files

| File | Description |
|------|-------------|
| [.cursor/rules/project-always.mdc](./.cursor/rules/project-always.mdc) | Always-applied Agent rules — copy to `.cursor/rules/` at your project root |
| [.cursor/rules/typescript.mdc](./.cursor/rules/typescript.mdc) | TypeScript-scoped rules (strict types, no `any`, ESLint + Prettier) |
| [.cursor/rules/python.mdc](./.cursor/rules/python.mdc) | Python-scoped rules (type annotations, ruff/black, pytest) |

## Native paths

Cursor scans for rules files in **`.cursor/rules/`** relative to the project root. The file extension must be **`.mdc`** and each file must include a YAML front-matter block:

```yaml
---
description: Short description shown in Cursor's rule picker
globs:               # optional — restrict rule to matching paths (e.g. "**/*.ts")
alwaysApply: true    # true = loaded for every Agent interaction; false = semantic match only
---
```

Rules **do not** work from arbitrary directories or with `.md`/`.markdown` extensions — the `.mdc` extension and front-matter are required.

## MCP Servers

Cursor supports [Model Context Protocol (MCP)](https://modelcontextprotocol.io) servers for giving the Agent access to external tools, APIs, and databases.

| Scope | Path | Notes |
|-------|------|-------|
| Project | `<repo-root>/.cursor/mcp.json` | Checked into version control; shared with the team |
| Global | `~/.cursor/mcp.json` | Available in all projects on this machine |

After adding a server, enable it in **Cursor Settings → MCP**.

## Background Agents

Cursor Background Agents run autonomously on GitHub issues and branches — no IDE session required. Enable under **Cursor Settings → Beta → Background Agent**. The agent opens a PR when the task is complete. Rules in `.cursor/rules/` are automatically available to background agent sessions.

## BugBot

Cursor BugBot performs automated PR reviews by scanning changes for bugs and regressions before you merge. Enable it in **Cursor Settings → BugBot** and connect your GitHub repository.

## Quickstart

Copy the full `.cursor/rules/` directory into your project root:

```bash
# Always-applied baseline
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/cursor/.cursor/rules/project-always.mdc \
  -o .cursor/rules/project-always.mdc

# Optional: TypeScript companion rules
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/cursor/.cursor/rules/typescript.mdc \
  -o .cursor/rules/typescript.mdc

# Optional: Python companion rules
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/cursor/.cursor/rules/python.mdc \
  -o .cursor/rules/python.mdc
```

For language-scoped rules, create additional `.mdc` files in the same directory with a `globs` key targeting the relevant file patterns (e.g. `**/*.ts`).
