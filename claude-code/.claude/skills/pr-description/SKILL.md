---
name: pr-description
description: "Use when the user wants to write, improve, or fill in a GitHub pull request description. Triggers: 'write a PR description', 'draft a PR', 'fill in the PR template', 'summarize this diff', or when the user pastes a diff / commits and asks for a PR body. Do NOT use for commit messages (use commit-message skill) or release notes."
---

# PR Description Writer

Write clear, reviewable GitHub PR descriptions.

## Format

```markdown
## What
One or two sentences. What does this PR change?

## Why
The problem or motivation. Link the issue if there is one (`Fixes #123`).

## How
Bullet points of the main implementation choices. Skip if the change is trivial.

## Testing
How it was verified. "Added unit tests", "Manually tested on staging", etc.

## Notes for reviewers
Optional. Call out anything non-obvious, risky, or that needs extra eyes.
```

Omit any section that has nothing useful to say.

## Rules

- Keep `## What` under 2 sentences. Reviewers scan this first.
- Link issues with `Fixes #N` or `Closes #N` so GitHub auto-closes them on merge.
- Prefer bullets over paragraphs in `## How`.
- Never just list files changed — reviewers can see the diff. Explain *decisions*.
- If the diff touches public APIs, call it out explicitly under `## Notes for reviewers`.
- Match the repo's existing PR tone if visible (formal vs casual).

## Workflow

1. If a `.github/PULL_REQUEST_TEMPLATE.md` exists in the repo, use it as the structure instead of the default above.
2. Read the diff or commit list. Ask for it if not provided.
3. Draft the PR body. Keep it under ~150 words unless the change is large.
4. If there are breaking changes, put a **⚠️ Breaking change** line at the top.