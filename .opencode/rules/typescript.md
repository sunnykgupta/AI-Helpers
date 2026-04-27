---
description: TypeScript and JavaScript coding conventions
globs: "**/*.{ts,tsx,js,jsx,mjs,mjsx}"
---

# TypeScript Conventions

These rules apply to `.ts`, `.tsx`, `.js`, `.jsx`, `.mjs`, `.mjsx` files.

## Types

- Enable `strict` mode in `tsconfig.json`; never disable `strictNullChecks`.
- Prefer `type` aliases for unions, intersections, and mapped types; use `interface` for object shapes that may be extended.
- No `any` — use `unknown` and narrow with type guards instead.
- No non-null assertions (`!`) — handle nullability explicitly.
- Export all domain types from a single barrel file (e.g., `types/index.ts`).
- Avoid `as` type casts; if a cast is unavoidable, add a comment explaining why.

## Functions & Modules

- Prefer named exports over default exports for easier rename-refactoring.
- Avoid `namespace` — use ES modules (`import`/`export`) instead.
- Mark callbacks and event handlers `async` only if they actually `await` something.
- Use PascalCase for types and camelCase for functions/variables.

## Null / Undefined Handling

- Prefer `undefined` over `null` in new code; `null` only when interfacing with APIs that return it.
- Use optional chaining (`?.`) and nullish coalescing (`??`) rather than `||` guards.

## Error Handling

- Never swallow exceptions silently — always handle or re-throw.
- Use custom error classes with descriptive names and properties.
- Error messages should include relevant context (input values, IDs, etc.).

## Linting & Formatting

- Use `eslint` with `@typescript-eslint/recommended`; do not suppress rules without a comment.
- Format with `prettier`; do not mix `prettier` and manual style fixes in the same commit.
- Run `tsc --noEmit` as part of the lint step for TypeScript projects.

## Naming

- Use descriptive names — no single-letter variables except in loops or lambdas.
- Prefix boolean variables with `is`, `has`, `should`, `can`.
- Use verb phrases for functions: `getUser`, `isAuthenticated`, `handleClick`.