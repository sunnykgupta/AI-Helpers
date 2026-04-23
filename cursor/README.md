# Cursor Helpers

This directory contains helper files and ways of working for [Cursor](https://www.cursor.com/).

## Files

| File | Description |
|------|-------------|
| [.cursor/rules/project-always.mdc](../.cursor/rules/project-always.mdc) | Always-applied Agent rules (place at `.cursor/rules/` in your project root) |

## Usage

Copy `.cursor/rules/project-always.mdc` into the `.cursor/rules/` directory at the root of your own project. Cursor will automatically load it for every Agent interaction thanks to the `alwaysApply: true` front-matter.

For language-scoped rules, create additional `.mdc` files in the same directory with a `globs` key targeting the relevant file patterns (e.g. `**/*.ts`).
