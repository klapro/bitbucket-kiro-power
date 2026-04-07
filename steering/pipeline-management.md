---
inclusion: manual
---

# Pipeline Management Workflow

## Checking Pipeline Status

- Use `listPipelineRuns` with workspace and repo slug to see recent pipeline executions (state, trigger type, branch, commit).
- Use `getPipelineRun` with the pipeline UUID for detailed info on a specific run.

## Investigating Failures

1. Call `getPipelineSteps` to list all steps in the pipeline run.
2. Identify the failed step.
3. Call `getPipelineStepLogs` to read the logs for the failed step.
4. Analyze the error output to determine the root cause.

## Triggering Pipelines

Use `runPipeline` to manually trigger a pipeline run. Specify the branch or tag, and optionally a custom pipeline target from your `bitbucket-pipelines.yml`.

## Stopping Pipelines

Use `stopPipeline` to cancel a running pipeline — useful when you've pushed a fix, a pipeline is stuck, or you triggered one by mistake.

## Common Patterns

### Check PR Pipeline Status

1. `getPullRequest` to get PR details.
2. `getPullRequestStatuses` to see associated pipeline results.
3. If failed, drill into the run with `getPipelineSteps` and `getPipelineStepLogs`.

### Deploy Workflow

1. `mergePullRequest` to merge the PR.
2. `runPipeline` to trigger the deployment pipeline on the target branch.
3. `getPipelineRun` to monitor deployment progress.
4. `getPipelineStepLogs` to verify deployment output.
