---
name: fix-merge-conflicts
description: Resolve merge conflicts in the working tree. Use when there are conflict markers in files after a merge or rebase.
---

# Fix Merge Conflicts

## Workflow

1. Run `git status` to list all files with conflicts
2. For each conflicted file:
   a. Read the file and identify all `<<<<<<<`, `=======`, `>>>>>>>` conflict markers
   b. Understand what each side (HEAD vs incoming) is trying to accomplish
   c. Resolve the conflict by combining or choosing the correct version
   d. Remove all conflict markers
3. After resolving all files, run `git add <files>` to mark them resolved
4. If in a rebase, run `git rebase --continue`; if in a merge, run `git commit`

## Resolution Strategy

- **Favor semantic correctness** over mechanical combination — understand what each side intended
- **Prefer the incoming change** when it is a refactor or rename that HEAD hasn't caught up with
- **Prefer HEAD** when the incoming change accidentally reverts a recent fix
- **Merge both** when each side adds something independent (e.g. new imports, new fields)
- When uncertain, ask before resolving

## Rules

- Never silently drop code from either side without explaining why
- Always verify the file compiles or parses after resolving (run `git diff --check`)
- Do not run `git checkout --theirs` or `--ours` as a blanket solution — resolve each conflict thoughtfully
