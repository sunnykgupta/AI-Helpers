# Changelog

All notable changes to the helper files in this repository are recorded here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Tool-specific entries are prefixed with the relevant tool name (e.g. **[Claude Code]**, **[Codex]**, **[Cursor]**).

> **Why track this?**
> Claude Code and Codex both ship breaking behaviour changes roughly every 6–8 weeks.
> Cursor rule semantics have also shifted across major versions.
> This file records what changed, when, and why — so teams can audit and update their copies.

---

## [Unreleased]

### Added
- `shared/AGENTS.md` — unified baseline rules (code style, error handling, testing, security, git, workflow, documentation) referenced by all tool-specific files.
- `cursor/.cursor/rules/typescript.mdc` — TypeScript-scoped Cursor rules (strict types, no `any`, ESLint + Prettier).
- `cursor/.cursor/rules/python.mdc` — Python-scoped Cursor rules (type annotations, ruff/black, pytest).
- `cursor/.cursor/rules/project-always.mdc` now lives under `cursor/` so it mirrors the path users copy into their own projects.
- Root `README.md` expanded with native-path documentation, curl quickstart one-liners, and `.mdc` front-matter notes.

### Changed
- `claude/` directory renamed to `claude-code/` for clarity.

---

## [2026-07-04]

### Added — Claude Code

- **Plugin system** — Claude Code now has a first-class plugin system. Plugins bundle custom commands, agents, skills, hooks, and MCP servers and can be installed with `/plugin install <name>` from the marketplace. Plugin structure documented in `claude-code/CLAUDE.md`.
- **Custom commands** — Markdown files placed in `.claude/commands/` become slash commands (e.g. `.claude/commands/commit.md` → `/commit`). Documented in the feature table.
- **Extended thinking** — `think` and `ultrathink` keywords in your message trigger deeper reasoning before responding. `ultrathink` is more intensive and token-heavy.
- **MCP integration** — MCP servers are added via `claude mcp add <name> <command>` and configured in `.mcp.json` (repo root) or `.claude/mcp.json`. Documented in the feature table and directory structure.
- **Updated hooks** — Replaced the outdated `"postEditFile"` hook example with the current event-based system (`PreToolUse`, `PostToolUse`, `Stop`, `SessionStart`) including a working `settings.json` snippet.
- **`.claude/` directory layout** — Added a reference table for `commands/`, `agents/`, `skills/`, `hooks/`, `settings.json`, and `mcp.json`.

### Added — Cursor

- **MCP servers** — Documented `.cursor/mcp.json` (project) and `~/.cursor/mcp.json` (global) in `cursor/README.md` and `cursor/.cursor/rules/project-always.mdc`.
- **Background agents** — Documented Cursor Background Agents (autonomous operation on GitHub issues without an open IDE) in `cursor/README.md` and `project-always.mdc`.
- **BugBot** — Documented Cursor BugBot automated PR review in `cursor/README.md`.

### Changed — README

- Extended the Claude Code native-paths table with a supplementary `.claude/` paths table (commands, agents, skills, hooks, settings, MCP).
- Extended the Cursor native-paths section with MCP configuration paths.

---

<!-- Add new entries above this line, newest first -->
<!-- Template:

## [YYYY-MM-DD]

### Added
### Changed
### Deprecated
### Removed
### Fixed

-->
