# AGENTS.md — OpenCode Ways of Working

> This file is automatically loaded by OpenCode in every session.
> It captures the **common rules** shared across all AI coding tools, extended with OpenCode-native features.
>
> **How to use this file:**
> - Copy sections into your tool-specific instruction file, or
> - Reference external files using the `@` syntax (e.g., `@.opencode/rules/typescript.md`).

---

## Build & Verify Commands

Fill in the commands that match your project's actual toolchain:

- Build:            `<your build command>`
- Test (single):    `<your single-test command>`
- Lint / typecheck: `<your lint command>`
- Dev server:       `<your dev-server command>`

Always run lint/typecheck after a series of edits.
Prefer running a single targeted test over the full suite for speed.

OpenCode can also run programmatic checks after completing a task. Configure these in `opencode.json`:

```json
{
  "instructions": ["AGENTS.md", ".opencode/rules/*.md"]
}
```

---

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
- Non-interactive diff: `git --no-pager diff` or `git diff | cat`.
- Do not commit build artifacts, `dist/`, `__pycache__/`, or untracked lock files.

## Workflow

- Keep changes minimal and scoped to the current task.
- Use `rg` for codebase search; use non-interactive flags on all shell commands.
- Before writing new code, search for similar existing patterns first.
- When the correct approach is unclear, stop and ask — do not guess.
- Explain the plan before writing code when the task spans more than two files.
- Use subagents for large file-read investigations to preserve main context.

## Documentation

- Documentation lives in docstrings/JSDoc of the functions or classes it describes.
- Separate docs files only for ADRs, onboarding guides, or cross-module architecture concepts.
- Never duplicate documentation across files — one canonical location.
- Document current state only; no changelogs or history in docstrings.
- Comment *why*, not *what* — never restate what the code already says.

## Skills

OpenCode should consult the skills in `.opencode/skills/` for the following tasks:

- **Writing commit messages** → use the `commit-message` skill. It follows Conventional Commits and helps keep commit history consistent.
- **Writing PR descriptions** → use the `pr-description` skill.
- **Code review** → use the `codereview` skill for comprehensive code analysis.

## Custom Agents

OpenCode has built-in agents (build, plan, general, explore). You can also define custom agents in `.opencode/agents/`:

- **`@code-reviewer`** — Read-only code review agent. Cannot edit files. Use for quick analysis without making changes.
- **`@review-runner`** — Full code review agent that runs linting, typechecks, and tests. Provides actionable feedback.

---

## OpenCode-Specific Reminders

### Plan Mode vs Build Mode

Press **Tab** to toggle between Plan and Build modes:
- **Plan mode** (read-only) — Analyze code, suggest changes, create plans without making modifications
- **Build mode** — Make actual file changes and run commands

### Skills

Use the `skill` tool to load a skill:

```
skill({ name: "commit-message" })
skill({ name: "pr-description" })
skill({ name: "codereview" })
```

Available skills are listed in the skill tool description.

### File References

Use `@path/to/file` to include a file's content inline in your message:

```
How is authentication handled in @src/api/auth.ts
```

### Referencing External Files

You can reference external rule files in `AGENTS.md`:

```
For TypeScript rules: @.opencode/rules/typescript.md
For Python rules: @.opencode/rules/python.md
```

### Agent Invocation

Invoke custom agents using `@` mention:

```
@code-reviewer analyze this PR for potential issues
@review-runner run a full check on the changed files
```

### `/init` Command

Run `/init` to scan your project and improve `AGENTS.md` in place with project-specific guidance.

### Override File

Create `AGENTS.local.md` in the repo root (gitignored) for personal preferences that should not be shared with the team.

### Layered Instruction Order

| Scope | File | Notes |
|-------|------|-------|
| Local | `AGENTS.md`, `CLAUDE.md` (traversed up) | First match wins |
| Global | `~/.config/opencode/AGENTS.md` | Fallback |
| Claude compat | `~/.claude/CLAUDE.md` | If no OpenCode global found |