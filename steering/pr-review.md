---
inclusion: manual
---

# Pull Request Review Workflow

## Finding a Pull Request

Use `getPullRequests` with the workspace and repo slug to list open PRs, or `getPullRequest` if you already know the PR ID.

## Understanding the Changes

1. Call `getPullRequestDiffStat` for a summary of files changed and lines added/removed.
2. Call `getPullRequestDiff` to read the actual code changes.
3. Call `getPullRequestCommits` to understand the commit history.

## Checking CI/CD Status

- Call `getPullRequestStatuses` to see build/CI results.
- If pipelines are failing, use `getPipelineSteps` and `getPipelineStepLogs` to investigate.

## Reviewing and Commenting

- Use `addPullRequestComment` for general comments on the PR.
- Use `addPullRequestComment` with inline parameters (file path, line number) for line-specific feedback.
- Use `createPullRequestTask` to create actionable tasks for the author.

## Making a Decision

- `approvePullRequest` — Approve the PR.
- `requestChanges` — Request changes before merging.
- `declinePullRequest` — Decline the PR.

## Following Up

- `resolveComment` — Mark addressed comments as resolved.
- `updatePullRequestTask` — Mark completed tasks.
- `removeChangeRequest` then `approvePullRequest` — Once satisfied with changes.
- `mergePullRequest` — Merge directly from Kiro once approved.
- For draft PRs, use `publishDraftPullRequest` when ready for review.
