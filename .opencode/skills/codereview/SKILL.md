---
name: codereview
description: "Use when the user asks to review code, perform a code review, analyze changes for issues, or review a PR/diff. Runs linting, typechecks, and tests to provide comprehensive feedback. Do NOT use for simple questions about code (use the explore agent instead)."
---

# Code Review Skill

Perform a comprehensive code review including static analysis and tests.

## Workflow

1. **Identify the scope** — Determine which files/changes to review
2. **Run linting** — Execute the lint command and parse output
3. **Run typecheck** — Execute type checking and parse output
4. **Run tests** — Execute relevant tests and parse output
5. **Analyze code** — Read the changed files for logic issues, security concerns, performance problems
6. **Summarize findings** — Group issues by severity (critical/warning/suggestion)

## Commands to Run

Always run these commands non-interactively:

```bash
# Lint (adjust command to match project)
npm run lint                    # or: ruff check . / golangci-lint run / etc.

# Type-check
npm run typecheck              # or: mypy . / tsc --noEmit

# Tests (target the affected module)
npm test                       # or: pytest / go test ./...
```

If a project does not have one of these commands, skip that step.

## Issue Categories

### Critical
- Security vulnerabilities (SQL injection, XSS, exposed secrets)
- Authentication/authorization bugs
- Data corruption risks
- Unhandled error paths that could crash

### Warnings
- Code smells (duplication, complex functions, unclear naming)
- Performance concerns (N+1 queries, unnecessary allocations)
- Missing error handling
- Type safety issues

### Suggestions
- Code style deviations from project conventions
- Missing documentation on public APIs
- Opportunities for abstraction/DRY
- Test coverage gaps (only if the task explicitly requires testing)

## Output Format

```
## Code Review Summary

### Critical Issues
- [file:line] Description of the issue and suggested fix

### Warnings
- [file:line] Description of the issue and suggested fix

### Suggestions
- [file:line] Description of the suggestion

### Test Results
- Lint: PASS/FAIL (summary of errors)
- Typecheck: PASS/FAIL (summary of errors)
- Tests: PASS/FAIL (summary of failures)

### Files Reviewed
- List of files that were analyzed
```

## Rules

- Only report issues that are actually present in the code — do not speculate
- Provide actionable fixes, not just criticism
- Check for security issues first (secrets, injection vulnerabilities)
- Verify tests actually test what they claim to test
- Mark style issues as suggestions, not blockers
- Do not require changes for subjective preferences