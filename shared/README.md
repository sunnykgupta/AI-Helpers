# Shared Helpers

This directory contains the **unified baseline** rules shared across all AI coding tools.

## Files

| File | Description |
|------|-------------|
| [AGENTS.md](./AGENTS.md) | Common ways of working: code style, error handling, testing, security, git, workflow, and documentation |

## Purpose

Rather than maintaining identical rules in three separate files, this baseline captures the conventions that apply regardless of which AI tool you are using. Tool-specific files build on top of it:

| Tool file | What it adds |
|-----------|--------------|
| `claude-code/CLAUDE.md` | Claude Code keyboard shortcuts, hooks, `@import` syntax, Plan Mode |
| `codex/AGENTS.md` | Codex layering order, `--ask-for-approval` workflow, programmatic checks |
| `cursor/.cursor/rules/project-always.mdc` | `.mdc` front-matter, `alwaysApply` flag, language-scoped companion rules |

## How to use

**Option 1 — Copy and paste** the sections you need into your tool-specific instruction file.

**Option 2 — Import (Claude Code only):** Reference this file from `CLAUDE.md` using the `@` import syntax:

```markdown
@shared/AGENTS.md
```

Claude Code will inline the content at load time.
