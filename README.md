# AI-Helpers

A collection of helper (`.md`) files for use across various Gen AI tools. The goal is to capture ways of working and reusable instructions so they can be shared and reused without starting from scratch every time.

## Supported Tools

| Tool | Directory | Description |
|------|-----------|-------------|
| [OpenAI Codex](https://openai.com/codex) | [`codex/`](./codex/) | `AGENTS.md` and other Codex helpers |
| [Cursor](https://www.cursor.com/) | [`cursor/`](./cursor/) | Cursor rules and helper files |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | [`claude/`](./claude/) | Claude Code helper files |

## Structure

```
AI-Helpers/
├── .cursor/
│   └── rules/
│       └── project-always.mdc   # Always-applied Cursor Agent rules
├── codex/
│   ├── README.md
│   └── AGENTS.md                # Agent instructions for OpenAI Codex
├── cursor/
│   └── README.md                # Usage guide for the Cursor rule file
└── claude/
    ├── README.md
    └── CLAUDE.md                # Agent instructions for Claude Code
```

## Usage

Browse to the directory for the tool you are using and copy or reference the helper files from there into your own projects.
