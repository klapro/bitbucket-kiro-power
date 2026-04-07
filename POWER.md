---
name: "bitbucket-kiro-power"
displayName: "Bitbucket for Kiro"
description: "Access Bitbucket Cloud and Server — manage repositories, pull requests, code reviews, pipelines, and more."
keywords:
  [
    "bitbucket",
    "atlassian",
    "repositories",
    "pull requests",
    "PRs",
    "pipelines",
    "code review",
    "branches",
    "git",
    "ci/cd",
  ]
---

# Bitbucket for Kiro

Access Bitbucket Cloud and Server directly from Kiro. Manage repositories, pull requests, code reviews, pipelines, and more through MCP without leaving your editor.

## Setup

### 1. Create a Bitbucket API Token

1. Go to [Bitbucket API Tokens](https://bitbucket.org/account/settings/api-tokens/)
2. Click "Create API token"
3. Select the scopes you need (repositories read/write, pull requests read/write, pipelines read/write)
4. Copy the generated token

### 2. Configure Your Credentials

After installing the power, add your credentials to `~/.kiro/settings/mcp.json` under the `powers.mcpServers` section. You only need to provide the environment variables — the power handles the server command automatically:

```json
{
  "powers": {
    "mcpServers": {
      "bitbucket-mcp": {
        "env": {
          "BITBUCKET_TOKEN": "<your-api-token>",
          "BITBUCKET_WORKSPACE": "your-workspace-slug"
        }
      }
    }
  }
}
```

> **Note:** Place this under `powers.mcpServers`, not the top-level `mcpServers`. You can alternatively use `BITBUCKET_USERNAME` + `BITBUCKET_PASSWORD` for legacy app password auth (deprecated, disabled June 2026).

### Environment Variables

| Variable              | Required | Description                                                |
| --------------------- | -------- | ---------------------------------------------------------- |
| `BITBUCKET_TOKEN`     | Yes\*    | API token (recommended)                                    |
| `BITBUCKET_USERNAME`  | Yes\*    | Your Bitbucket username (legacy auth)                      |
| `BITBUCKET_PASSWORD`  | Yes\*    | App password (legacy, deprecated June 2026)                |
| `BITBUCKET_WORKSPACE` | No       | Default workspace slug                                     |
| `BITBUCKET_URL`       | No       | API base URL (defaults to `https://api.bitbucket.org/2.0`) |

\*Use `BITBUCKET_TOKEN` or `BITBUCKET_USERNAME` + `BITBUCKET_PASSWORD`.

### Optional Variables

| Variable                     | Description                     |
| ---------------------------- | ------------------------------- |
| `BITBUCKET_ENABLE_DANGEROUS` | Enable destructive operations   |
| `BITBUCKET_LOG_DISABLE`      | Disable logging                 |
| `BITBUCKET_LOG_FILE`         | Custom log file path            |
| `BITBUCKET_LOG_DIR`          | Custom log directory            |
| `BITBUCKET_LOG_PER_CWD`      | Per-working-directory log files |

## Available Tools

### listRepositories

List repositories in a workspace.

### getRepository

Get details of a specific repository.

### getPullRequests

List pull requests for a repository.

### createPullRequest

Create a new pull request.

### getPullRequest

Get detailed information about a specific pull request.

### updatePullRequest

Update PR title, description, or reviewers.

### approvePullRequest / unapprovePullRequest

Approve or remove approval from a pull request.

### declinePullRequest

Decline a pull request.

### mergePullRequest

Merge a pull request.

### requestChanges / removeChangeRequest

Request changes on a PR or remove a change request.

### createDraftPullRequest / publishDraftPullRequest / convertToDraft

Manage draft pull requests.

### getPullRequestComments

List all comments on a pull request.

### addPullRequestComment

Add a comment to a PR. Supports inline comments on specific files and lines.

### getPullRequestComment / updatePullRequestComment / deletePullRequestComment

Manage individual PR comments.

### resolveComment / reopenComment

Resolve or reopen comment threads.

### getPullRequestDiff / getPullRequestDiffStat / getPullRequestPatch

View PR diffs, diffstat summaries, and patches.

### getPullRequestTasks

List tasks on a pull request.

### createPullRequestTask / getPullRequestTask / updatePullRequestTask / deletePullRequestTask

Manage PR review tasks.

### getPullRequestCommits

List commits in a pull request.

### getPullRequestStatuses

Get build/CI statuses for a pull request.

### getPullRequestActivity

Get the activity feed for a pull request.

### listPipelineRuns

List pipeline runs for a repository.

### getPipelineRun

Get details of a specific pipeline run.

### runPipeline

Trigger a new pipeline run.

### stopPipeline

Stop a running pipeline.

### getPipelineSteps / getPipelineStep

Inspect pipeline steps.

### getPipelineStepLogs

View logs for a pipeline step.

## Example Prompts

- "List all repositories in my workspace"
- "Show me open pull requests for repo my-app"
- "Create a PR from feature/login to main"
- "Approve PR #42 in my-app"
- "Show me the diff for PR #15"
- "Add an inline comment on line 25 of src/index.ts in PR #42"
- "What's the pipeline status for the latest run?"
- "Trigger a pipeline on the main branch"
- "Show me the logs for the failed pipeline step"

## Tips

- Use `getPullRequestDiffStat` for a quick overview before diving into the full diff
- To review a PR end-to-end, use the `pr-review` steering guide
- For pipeline troubleshooting, use the `pipeline-management` steering guide
- Call `getPullRequestStatuses` to check CI before merging
