# CLAUDE.md — Claude Code Ways of Working

> This file is automatically loaded by Claude Code in every session. Personal overrides go in `CLAUDE.local.md` (gitignored).

---

## Build & Verify Commands

- Build:            `<your build command>`
- Test (single):    `<your single-test command>`
- Lint / typecheck: `<your lint command>`
- Dev server:       `<your dev-server command>`

Always run the lint/typecheck command after a series of edits.
Prefer running a single targeted test over the full suite for speed.

## Code Style

- Prefer functional programming over OOP; use classes only for connectors and interfaces to external systems.
- Write pure functions — return new values, never mutate input parameters or global state.
- Write single-purpose functions — no multi-mode behaviour, no flag parameters that switch logic branches.
- Never use default parameter values — make all parameters explicit at the call site.
- Create named type definitions for complex data structures; no anonymous inline shapes crossing function boundaries.
- Before writing new logic, search with `rg` for existing implementations.
- Follow YAGNI — do not add abstractions for speculative future use cases.

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

## Security — NEVER

- Commit secrets, API keys, tokens, passwords, or `.env` files.
- Force-push to `main`, `master`, or any protected branch.
- Add new external dependencies without asking first.
- Log or print PII, credentials, or tokens.
- Build SQL queries or shell commands via string concatenation.

## Security — ASK FIRST

- Adding any new external dependency.
- Running database migrations.
- Deleting or renaming files.
- Modifying CI/CD configs or deployment definitions.
- Touching authentication or authorization logic.

## Git

- Conventional commits: `type(scope): description`
  Valid types: `feat` `fix` `refactor` `test` `chore` `docs`
- Atomic commits — one logical change per commit.
- Branch naming: `type/short-description`.
- Non-interactive diff always: `git --no-pager diff` or `git diff | cat`.

## Workflow

- Keep changes minimal and scoped to the current task.
- Before writing new code, spend time searching for similar existing patterns.
- When the correct approach is unclear, stop and ask — do not guess.
- Explain the plan before writing code when the task spans more than two files.
- Use subagents for large file-read investigations to preserve main context.
- Use hooks for actions that must happen every time without exception
  (configure in `.claude/settings.json` or run `/hooks`).

## Documentation

- Documentation lives in docstrings/JSDoc of the functions or classes it describes.
- Separate docs files only for ADRs, onboarding guides, or cross-module architecture concepts.
- Never duplicate documentation across files — one canonical location.
- Document current state only; no changelogs or history in docstrings.
- Comment *why*, not *what* — never restate what the code already says.

## Skills

Claude should consult the skills in `.claude/skills/` for the following tasks:

Writing commit messages → use the commit-message skill. It follows our team's Conventional Commits convention and helps keep commit history consistent.
Writing PR descriptions → use the pr-description skill.

---

## Claude Code-Specific Reminders

| Feature | Usage |
|---------|-------|
| **Compact / Clear context** | `/compact` summarises and continues; `/clear` resets entirely. Use between unrelated tasks. |
| **Plan Mode** | Press **Ctrl+G** to enter Plan Mode — Claude proposes a plan before writing any code. Use for tasks spanning multiple files. |
| **Skills** | Invoke a skill with `/skill-name` (e.g. `/codereview`, `/explain`). Skills are predefined prompt pipelines. |
| **File references** | Use `@path/to/file` to include a file's content inline in your message (e.g. `@src/api/users.ts`). |
| **Imports in CLAUDE.md** | Use `@path/to/other.md` to compose multiple instruction files (e.g. `@.claude/security.md`). Claude Code-only syntax. |
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
