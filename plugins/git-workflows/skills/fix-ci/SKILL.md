---
name: fix-ci
description: Diagnose and fix CI failures on the current branch using the GitHub CLI. Use when CI is broken and needs debugging.
---

# Fix CI

## Workflow

1. Identify the current branch with `git branch --show-current`
2. Find the open PR for this branch with `gh pr view --json number,url,statusCheckRollup`
3. Identify which check is failing from the rollup
4. Fetch the failed job logs with `gh run view <run-id> --log-failed`
5. Read the error output carefully to identify the root cause
6. If nothing is broken, report that and stop
7. Form a plan — explain what you believe is wrong and how you'll fix it
8. Apply the fix
9. Summarize what was changed and why

## Rules

- Do not guess — read the actual logs before proposing a fix
- Fix one issue at a time; re-run CI to verify before tackling the next
- If the failure is in a flaky test or external dependency, flag that instead of patching around it
- Always explain the root cause, not just the symptom
