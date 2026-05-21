---
name: senior-review-merge
description: Reviews unmerged junior issue branches, requests fixes or merges when safe, and reconciles linked issues. Use only in a GPT-5.5 session when the user asks to review, approve, or merge junior/Spark agent work.
---

# Senior Review Merge

This skill is reserved for GPT-5.5. If the current session is not GPT-5.5, or the model is unknown, stop and say this workflow requires a GPT-5.5 reviewer.

## Contract

- Review as maintainer, not implementer.
- Discover junior work from unmerged `issue-*` branches, not from markdown status on `main`.
- Do not approve your own branch or a branch from the same implementation session.
- Do not merge unless the user explicitly asked for merge/approve-and-merge.
- Reconcile the issue with shipped reality before closing it.
- Production deploys and database writes remain separate explicit actions.

## Review Workflow

1. Fetch remote branches.
2. List unmerged remote branches matching `origin/issue-*`.
3. For each branch selected for review, infer the issue number from the branch name and read the issue file.
4. Inspect the diff against `origin/main` for correctness, scope control, security, data loss, and missing tests.
5. Run the smallest meaningful local checks.
6. Verify the branch satisfies the issue acceptance criteria.
7. If not safe, leave concrete blockers in a coordination issue/comment and do not merge.
8. If safe and merge was requested, merge locally into `main` or create/merge a PR only if the repo requires it.
9. Mark the issue `Status: done` and tick shipped acceptance criteria only after the merge reflects what actually shipped.
10. Delete the merged issue branch locally/remotely if the user wants branch cleanup.

## Merge Gate

Merge only if all are true:

- Worktree is clean.
- Required tests for the changed surface passed locally or in CI.
- Diff is scoped to the issue.
- No production deploy, DB migration, or env mutation is hidden inside the PR.
- The branch is up to date enough that conflicts and stale assumptions are understood.

## Output

Report:

- review decision
- checks run
- merge SHA if merged
- issue update/closure status
- branch cleanup status
- remaining risks
