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

<!-- Add new entries above this line, newest first -->
<!-- Template:

## [YYYY-MM-DD]

### Added
### Changed
### Deprecated
### Removed
### Fixed

-->
