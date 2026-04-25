---
description: Python coding conventions
globs: "**/*.py"
---

# Python Conventions

These rules apply to all `.py` files.

## Type Annotations

- Use `py.typed` marker file to indicate PEP 561 compliance.
- Use `mypy --strict` or equivalent; no `Any` without explicit justification.
- Prefer `typing.Optional[T]` over `T | None`.
- Use `typing.Sequence[T]` for read-only sequences, `typing.List[T]` when mutation is needed.

## Functions

- Prefer pure functions; avoid modifying global state or input parameters.
- Use keyword-only arguments for parameters with complex defaults.
- Return type annotations required for public APIs, encouraged for private functions.

## Error Handling

- Never use bare `except:` — catch specific exceptions.
- Use custom exceptions inheriting from appropriate built-in classes.
- Error messages should include relevant context for debugging.

## Testing

- Use `pytest`; follow existing test patterns in the codebase.
- Name test files `test_<module>.py` or `<module>_test.py`.
- Use descriptive test names: `test_user_cannot_login_with_wrong_password`.
- Fixtures should be explicit, not hidden in global setup.

## Linting & Formatting

- Use `ruff` for linting and formatting; it's faster than separate tools.
- Use `black` for formatting if `ruff` is not configured for formatting.
- Run `ruff check` and `ruff format` before committing.

## Naming

- `snake_case` for functions, methods, variables, parameters.
- `PascalCase` for classes, exceptions, type aliases.
- `SCREAMING_SNAKE_CASE` for module-level constants.
- Prefix private functions with `_` but avoid `__` name mangling.