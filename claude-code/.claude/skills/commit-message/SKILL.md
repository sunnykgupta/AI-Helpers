---
name: commit-message
description: "Use when the user wants to write a git commit message — including 'write a commit message', 'commit this', or when they paste a diff / staged changes and ask what to commit it as. Follows Conventional Commits. Do NOT use for PR descriptions (use pr-description skill)."
---

# Commit Message Writer

Write commit messages that follow [Conventional Commits](https://www.conventionalcommits.org/).

## Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

- **type** (required): one of `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`
- **scope** (optional): the module/area touched, e.g. `auth`, `api`, `parser`
- **subject** (required): imperative mood, lowercase, no period, ≤ 50 chars
- **body** (optional): wrap at 72 chars, explain *why* not *what*
- **footer** (optional): `BREAKING CHANGE: ...` or `Closes #123`

## Rules

- Subject line in imperative mood: "add login form", not "added" or "adds".
- Blank line between subject and body, and between body and footer.
- Use `!` after type/scope for breaking changes: `feat(api)!: drop v1 endpoints`.
- One commit = one logical change. If the diff covers multiple concerns, suggest splitting.
- Never put file names in the subject. Use scope instead.

## Workflow

1. Ask for the diff or `git status` output if not provided.
2. Determine type from the nature of the change (new feature → `feat`, bugfix → `fix`, etc.).
3. Pick a scope from the most-touched directory or module.
4. Write subject, then body only if context is non-obvious.
5. Add `BREAKING CHANGE:` footer if applicable.

## Examples

```
feat(auth): add OAuth login via GitHub

Users can now sign in with their GitHub account. Uses the standard
OAuth2 flow; tokens are stored in httpOnly cookies.

Closes #142
```

```
fix(parser): handle empty input without crashing
```

```
refactor(api)!: rename /users endpoint to /accounts

BREAKING CHANGE: /users is removed. Update clients to use /accounts.
```