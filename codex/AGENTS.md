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

- After any code change: `<your lint/typecheck command>`
- After logic changes: `<your test command for the affected module>`
- After dependency changes: verify lock file is updated

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

## Build & Run Commands

- Build:            `<your build command>`
- Test (single):    `<your single-test command>`
- Lint / typecheck: `<your lint command>`
- Dev server:       `<your dev-server command>`

## Code Style

- Prefer functional programming over OOP; use classes only for connectors and interfaces to external systems.
- Write pure functions — return new values, never mutate input parameters or global state.
- Write single-purpose functions — no multi-mode behaviour, no flag parameters that switch logic branches.
- Never use default parameter values — make all parameters explicit at the call site.
- Create named type definitions for complex data structures; no anonymous inline shapes crossing function boundaries.
- Before writing new logic, search with `rg` for existing implementations.
- Follow YAGNI — do not add abstractions for speculative future use cases.
- Keep diffs small; prefer targeted edits over wide refactors unless the full refactor is the explicit task.

## Error Handling

- Raise errors explicitly at the point of failure; never swallow exceptions silently.
- Use specific error types; avoid generic catch-alls that hide root causes.
- Fix root causes, not symptoms; no workaround shims unless the root fix is out of scope.
- No fallbacks or degraded-mode logic unless explicitly requested.
- External service calls: retry with exponential backoff, log each retry as a warning, re-raise the last error.
- Error messages must include: request params, response body, status codes, correlation IDs.
- Use structured logging fields — do not interpolate dynamic values into message strings.

## Testing

- Match the existing test strategy; do not introduce new frameworks without discussion.
- Do not add tests unless the task explicitly requires them.
- Prefer integration or end-to-end tests over unit tests.
- Avoid mocks when real service calls are practical.
- Unit tests are acceptable for pure data-transformation functions only.
- Never add tests to increase coverage numbers.
- Add the minimum test surface area for the current change.

## Security — NEVER

- Commit secrets, API keys, tokens, passwords, or `.env` files.
- Force-push to `main`, `master`, or any protected branch.
- Add new external dependencies without asking first.
- Delete files outside the project directory.
- Log or print PII, credentials, or tokens.
- Build SQL queries or shell commands via string concatenation.

## Security — ASK FIRST

- Adding any new external dependency (explain what it replaces).
- Running database migrations.
- Deleting or renaming files.
- Modifying CI/CD configs or deployment definitions.
- Touching authentication or authorization logic.

## Security — ALWAYS

- Validate and sanitize external input before use in queries, shell calls, or file paths.
- Use parameterized queries for all database interactions.
- Reference secrets by environment variable name, never by value.

## Git

- Conventional commits: `type(scope): description`
  Valid types: `feat` `fix` `refactor` `test` `chore` `docs`
- Atomic commits — one logical change per commit.
- Branch naming: `type/short-description`.
- Non-interactive diff always: `git --no-pager diff` or `git diff | cat`.
- Do not commit build artifacts, `dist/`, `__pycache__/`, or untracked lock files.

## Workflow

- Keep changes minimal and scoped to the current task.
- Use `rg` for codebase search; use non-interactive flags on all shell commands.
- Before writing new code, search for similar existing patterns first.
- When the correct approach is unclear, stop and ask — do not guess.
- Explain the plan before writing code when the task spans more than two files.

## Documentation

- Documentation lives in docstrings/JSDoc of the functions or classes it describes.
- Separate docs files only for ADRs, onboarding guides, or cross-module architecture concepts.
- Never duplicate documentation across files — one canonical location.
- Document current state only; no changelogs or history in docstrings.
- Comment *why*, not *what* — never restate what the code already says.

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
