# AI-Helpers

A collection of helper (`.md` / `.mdc`) files for use across various Gen AI coding tools. The goal is to capture ways of working and reusable instructions so they can be shared and reused without starting from scratch every time.

## Supported Tools

| Tool | Directory | Instruction file |
|------|-----------|-----------------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | [`claude-code/`](./claude-code/) | `CLAUDE.md` |
| [OpenAI Codex](https://openai.com/codex) | [`codex/`](./codex/) | `AGENTS.md` |
| [Cursor](https://www.cursor.com/) | [`cursor/`](./cursor/) | `.cursor/rules/*.mdc` |
| [OpenCode](https://opencode.ai) | [`..opencode/`](./..opencode/) | `AGENTS.md` |

## Structure

```
AI-Helpers/
├── README.md
├── CHANGELOG.md
├── shared/
│   └── AGENTS.md                          ← unified baseline (code style, security, git, etc.)
├── claude-code/
│   ├── README.md
│   └── CLAUDE.md                          ← Claude Code instruction file
├── codex/
│   ├── README.md
│   └── AGENTS.md                          ← Codex instruction file
├── cursor/
│   ├── README.md
│   └── .cursor/
│       └── rules/
│           ├── project-always.mdc         ← always-applied baseline rules
│           ├── typescript.mdc             ← TypeScript-scoped companion rules
│           └── python.mdc                 ← Python-scoped companion rules
├── ..opencode/
│   ├── AGENTS.md                          ← OpenCode instruction file
│   ├── README.md
│   ├── skills/                       ← reusable skills (PR descriptions, commits, code review)
│   ├── agents/                        ← custom agents (code-reviewer, review-runner)
│   └── rules/                         ← language-scoped rules (TypeScript, Python)
```

## Native paths

Each tool reads instruction files from specific locations. Understanding the difference between **global** and **project-level** paths lets you decide where to install a file.

### Claude Code — `CLAUDE.md`

| Scope | Path | Notes |
|-------|------|-------|
| Global | `~/.claude/CLAUDE.md` | Applies to every Claude Code session on this machine |
| Project | `<repo-root>/CLAUDE.md` | Checked into version control; shared with the team |
| Local override | `<repo-root>/CLAUDE.local.md` | Gitignored; personal preferences not shared with the team |

### Codex — `AGENTS.md`

| Scope | Path | Notes |
|-------|------|-------|
| Global | `~/.codex/AGENTS.md` | Applies to every Codex session on this machine |
| Repo root | `<repo-root>/AGENTS.md` | Checked into version control; shared with the team |
| Subdirectory | `<dir>/AGENTS.md` | Scoped to tasks within that directory |
| Override | `<repo-root>/AGENTS.override.md` | Gitignored; local overrides merged on top |

### Cursor — `.mdc` rule files

Cursor rules live in **`.cursor/rules/`** relative to the project root. Two important requirements:

1. The file extension **must be `.mdc`** — `.md` or `.markdown` files are ignored.
2. Each file **must start with a YAML front-matter block**:

```yaml
---
description: Short description shown in Cursor's rule picker
globs:               # optional — restrict rule to matching file patterns (e.g. "**/*.ts")
alwaysApply: true    # true = loads for every Agent interaction; false = semantic match only
---
```

### OpenCode — `AGENTS.md` / `AGENTS.local.md`

OpenCode reads `AGENTS.md` from multiple locations with layered precedence:

| Scope | Path | Notes |
|-------|------|-------|
| Project | `<repo-root>/AGENTS.md` | Checked into version control; shared with the team |
| Project | `<repo-root>/AGENTS.local.md` | Gitignored; personal overrides |
| Global | `~/.config/opencode/AGENTS.md` | Applies to every OpenCode session on this machine |

OpenCode also supports Claude Code-compatible instruction files: project-level `CLAUDE.md` (that is, `<repo-root>/CLAUDE.md`) and global `~/.claude/CLAUDE.md`. Skills live in `.opencode/skills/<name>/SKILL.md` (project) or `~/.config/opencode/skills/<name>/SKILL.md` (global).

## Quickstart

Copy the file(s) for your tool directly into your project with a single `curl` command.

**Claude Code**
```bash
# Project-level (add to your repo)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/claude-code/CLAUDE.md \
  -o CLAUDE.md

# Global (applies to all your projects)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/claude-code/CLAUDE.md \
  -o ~/.claude/CLAUDE.md
```

**Codex**
```bash
# Project-level (add to your repo)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/codex/AGENTS.md \
  -o AGENTS.md

# Global (applies to all your projects)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/codex/AGENTS.md \
  -o ~/.codex/AGENTS.md
```

**Cursor**
```bash
mkdir -p .cursor/rules

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

**OpenCode**
```bash
# Project-level (add to your repo)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/AGENTS.md \
  -o AGENTS.md

# Global (applies to all your projects)
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/AGENTS.md \
  -o ~/.config/opencode/AGENTS.md

# Optional: Skills (commit-message, pr-description, codereview)
mkdir -p ..opencode/skills
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/skills/commit-message/SKILL.md \
  -o ..opencode/skills/commit-message/SKILL.md
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/skills/pr-description/SKILL.md \
  -o ..opencode/skills/pr-description/SKILL.md
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/skills/codereview/SKILL.md \
  -o ..opencode/skills/codereview/SKILL.md

# Optional: Custom agents (code-reviewer, review-runner)
mkdir -p ..opencode/agents
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/agents/code-reviewer.md \
  -o ..opencode/agents/code-reviewer.md
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/agents/review-runner.md \
  -o ..opencode/agents/review-runner.md

# Optional: Language-scoped rules (TypeScript, Python)
mkdir -p ..opencode/rules
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/rules/typescript.md \
  -o ..opencode/rules/typescript.md
curl -fsSL https://raw.githubusercontent.com/sunnykgupta/AI-Helpers/main/.opencode/..opencode/rules/python.md \
  -o ..opencode/rules/python.md
```

## Shared baseline

[`shared/AGENTS.md`](./shared/AGENTS.md) is the **common source of truth** for rules that apply regardless of which AI tool you are using (code style, error handling, testing, security, git, workflow, documentation). The tool-specific files extend it with tool-native features and reminders.

## Contributing

See [`CHANGELOG.md`](./CHANGELOG.md) for a history of changes to the helper files. When updating rules, add an entry there so teams can audit what changed and update their copies.

