# AGENTS.md — OpenAI Codex Ways of Working

> Codex reads AGENTS.md files in a layered order:
> 1. Global: `~/.codex/AGENTS.md`
> 2. Repo root: `./AGENTS.md`
> 3. Subdirectory: any `AGENTS.md` found in sub-folders relevant to the task
>
> Each layer adds to (or overrides) the previous one. For project-specific overrides, use `AGENTS.override.md` in the repo root — it is merged on top of this file without replacing it.

---

## Programmatic Checks

Codex will attempt to run the following commands after completing a task. All checks must pass before the task is considered done. Adjust these commands to match the project's actual toolchain.

```bash
# Lint
npm run lint         # or: ruff check . / golangci-lint run / etc.

# Type-check (if applicable)
npm run typecheck    # or: mypy . / tsc --noEmit

# Tests
npm test             # or: pytest / go test ./...

# Build (if applicable)
npm run build
```

If a project does not have one of these scripts, skip that step — do not create placeholder scripts.

---

## Code Style

- Follow the conventions already present in the codebase. Do not introduce new patterns without discussion.
- Prefer explicit, readable code over clever one-liners.
- Keep functions small and single-purpose.
- Respect existing linter and formatter configuration files (`.eslintrc`, `pyproject.toml`, `.prettierrc`, etc.).

## Error Handling

- Never swallow exceptions silently. Log or re-raise with context.
- Distinguish recoverable errors (return/log) from unrecoverable ones (raise/exit).
- Validate all inputs at public boundaries.
- Use structured error types where the language supports it.

## Testing

- Write or update tests for every behaviour change.
- Unit tests cover logic; integration tests cover I/O boundaries.
- All tests must pass before a task is marked complete.
- No placeholder `assert True` / no-op tests.

## Security

- Never hardcode secrets, tokens, or credentials — use environment variables or a secrets manager.
- Sanitise all user-supplied input before use in queries, shell commands, or HTML.
- Apply the principle of least privilege.
- Flag dependency changes that affect security-sensitive packages.

## Git

- Commit messages in the imperative mood: *"Fix null-check in auth middleware"*.
- One logical change per commit.
- Branch names: `feat/<topic>`, `fix/<topic>`, `chore/<topic>`.
- Do not force-push to shared branches.

## Documentation

- Update docstrings and comments whenever behaviour changes.
- Update README when public interfaces, environment variables, or setup steps change.
- Add comments only where intent is non-obvious — prefer self-documenting code.

---

## Codex-Specific Reminders

### `--ask-for-approval` Workflow

When running Codex with `--ask-for-approval`, it will pause before executing any shell command that has side effects (file writes, network calls, installs). Review each proposed command before approving. This is the recommended mode for production or shared environments.

### Override File

`AGENTS.override.md` (repo root, gitignored) is merged on top of this file. Use it for:
- Personal tool preferences that should not be shared
- Temporary rule changes during an experiment
- Local environment-specific commands

### Layered Instruction Order

| Scope | File | Notes |
|-------|------|-------|
| Global | `~/.codex/AGENTS.md` | Applies to all projects on this machine |
| Repo root | `./AGENTS.md` | This file — shared with the team via version control |
| Subdirectory | `<dir>/AGENTS.md` | Scoped to tasks within that directory |
| Override | `./AGENTS.override.md` | Local overrides; gitignored |
