---
name: create-pr
description: Create a pull request with a formatted description and open it in the browser. Use when ready to open a PR.
---

# Create PR

## Preconditions

1. Confirm you are NOT on `main` or `master`. If you are, create a new branch first.
2. If there are uncommitted changes (staged or unstaged), commit them before opening the PR.

## PR Format

**Title** (80 chars or less):
```
<area>: <what changed>
```

**Body**:
```
## Summary
<1–2 sentence TLDR>

## Changes
- Bullet point describing change 1
- Bullet point describing change 2
- Bullet point describing change 3
```

## Workflow

1. Run `git log main..HEAD --oneline` to see all commits on this branch
2. Run `git diff main...HEAD --stat` to understand the scope of changes
3. Draft the title and body following the format above
4. Use `gh pr create --title "..." --body "..."` to open the PR
5. Include the PR link in your response as a clickable markdown link: `[PR #N: Title](url)`
6. Run `open <url>` to open the PR in the browser

## Rules

- Prepend `GIT_EDITOR=true` to git commands that may open an editor
- Always show the PR link in your final response
- Keep the title under 80 characters
- Limit the body to 3 bullet points unless the change is unusually large
