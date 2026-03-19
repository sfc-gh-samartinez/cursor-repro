---
name: git-commit
description: Create a conventional commit message from staged changes and run git commit. Use when asked to commit, write a commit message, or create a commit.
---

# Git Commit

## When to Use

- User asks to commit staged changes
- User wants a commit message or to create a commit
- User asks to summarize what will be committed (then offer to commit)

## Conventional Commit Format

```
<type>(<scope>): <subject>
```

**Type** (required): `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

**Scope** (optional): affected area, e.g. `auth`, `api`, `ui`

**Subject** (required): imperative mood, lowercase, no period, under ~50 chars

## Examples

```
feat(auth): add OAuth2 login flow
fix(api): handle null response from payments endpoint
refactor(db): extract query builder to separate module
chore: update dependencies
docs: add setup instructions to README
```

## Workflow

1. Run `git diff --staged` and `git status` to inspect changes
2. Infer type and scope from the diff
3. Write a single-line subject in imperative mood
4. Run `git commit -m "<message>"` to create the commit

## Rules

- One line only — no body or footer unless the user asks for it
- Subject under ~50 characters; omit scope if the message stays clear without it
- No period at the end
- Actually run `git commit` — do not just suggest the message
- Only commit when instructed; do not keep committing subsequent work
- Offer to push only if not on `main` or `master`
