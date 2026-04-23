# Cursor Helpers

This directory contains helper files and ways of working for [Cursor](https://www.cursor.com/).

## Files

| File | Description |
|------|-------------|
| [.cursor/rules/project-always.mdc](./.cursor/rules/project-always.mdc) | Always-applied Agent rules — copy to `.cursor/rules/` at your project root |
| [.cursor/rules/typescript.mdc](./.cursor/rules/typescript.mdc) | TypeScript-scoped rules (strict types, no `any`, ESLint + Prettier) |
| [.cursor/rules/python.mdc](./.cursor/rules/python.mdc) | Python-scoped rules (type annotations, ruff/black, pytest) |

## Native paths

Cursor scans for rules files in **`.cursor/rules/`** relative to the project root. The file extension must be **`.mdc`** and each file must include a YAML front-matter block:

```yaml
---
description: Short description shown in Cursor's rule picker
globs:               # optional — restrict rule to matching paths (e.g. "**/*.ts")
alwaysApply: true    # true = loaded for every Agent interaction; false = semantic match only
---
```

Rules **do not** work from arbitrary directories or with `.md`/`.markdown` extensions — the `.mdc` extension and front-matter are required.

## Quickstart

Copy the full `.cursor/rules/` directory into your project root:

```bash
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

For language-scoped rules, create additional `.mdc` files in the same directory with a `globs` key targeting the relevant file patterns (e.g. `**/*.ts`).
