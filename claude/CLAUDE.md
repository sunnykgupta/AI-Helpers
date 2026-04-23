# CLAUDE.md — Claude Code Ways of Working

> This file is automatically loaded by Claude Code in every session. Personal overrides go in `CLAUDE.local.md` (gitignored).

---

## Code Style

- Use the language and framework conventions already established in the project — don't introduce new patterns without discussion.
- Prefer explicit over implicit: clear variable names, obvious control flow, no magic numbers.
- Keep functions and methods small and single-purpose.
- Format code consistently; defer to any existing linter/formatter config (`.eslintrc`, `pyproject.toml`, etc.).

## Error Handling

- Never swallow exceptions silently. Log or re-raise with context.
- Distinguish between recoverable errors (return/log) and unrecoverable ones (raise/exit).
- Validate inputs at boundaries (API handlers, CLI entry points, public functions).
- Prefer structured error types over bare string messages where the language supports it.

## Testing

- Write or update tests for every behaviour change, not just new features.
- Favour unit tests for logic and integration tests for I/O boundaries.
- Tests must pass before a task is considered done — don't leave them red.
- Prefer real assertions over `assert True` / no-op placeholders.

## Security

- Never hardcode secrets, tokens, or credentials — use environment variables or a secrets manager.
- Sanitise all user-supplied input before use in queries, shell commands, or HTML output.
- Apply the principle of least privilege: request only the permissions the code actually needs.
- Flag any dependency updates that touch security-sensitive packages.

## Git

- Write commit messages in the imperative mood: *"Add rate limiter"*, not *"Added rate limiter"*.
- Keep commits atomic — one logical change per commit.
- Branch names: `feat/<topic>`, `fix/<topic>`, `chore/<topic>`.
- Do not force-push to shared branches.

## Documentation

- Update docstrings and inline comments when behaviour changes.
- README changes are required whenever a public interface, environment variable, or setup step changes.
- Prefer self-documenting code; add comments only where intent is non-obvious.

---

## Claude Code-Specific Reminders

| Feature | Usage |
|---------|-------|
| **Compact context** | Run `/compact` when the context grows large to summarise and continue efficiently. |
| **Clear context** | Run `/clear` to start a completely fresh context (use when switching to an unrelated task). |
| **Plan Mode** | Press **Ctrl+G** to enter Plan Mode — Claude proposes a plan before writing any code. Use this for large or risky tasks. |
| **Skills** | Invoke a skill with `/skill-name` (e.g. `/codereview`, `/explain`). Skills are predefined prompt pipelines. |
| **File references** | Use `@path/to/file` to include a file's content inline in your message (e.g. `@src/api/users.ts`). |
| **Imports in CLAUDE.md** | Use `@path/to/other.md` to compose multiple instruction files (e.g. `@.claude/security.md`). |
| **Subagents** | For large investigations spanning many files or modules, ask Claude to launch a subagent rather than cramming everything into one context. |

### Hooks vs CLAUDE.md Instructions

For actions that must **always** happen without exception (e.g. running a linter after every edit, blocking a specific shell command), prefer **hooks** defined in `.claude/settings.json` over instructions in this file. Hooks are deterministic and enforced programmatically; CLAUDE.md instructions are best-effort guidance.

```jsonc
// .claude/settings.json (example)
{
  "hooks": {
    "postEditFile": ["npm run lint --fix"]
  }
}
```

### Personal Overrides

Create `CLAUDE.local.md` in the repo root (gitignored) for personal preferences that should not be shared with the team — e.g. preferred verbosity level, personal tool aliases, or experimental flags.
