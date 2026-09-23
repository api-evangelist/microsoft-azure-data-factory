---
name: microsoft-azure-data-factory-run-a-pipeline
description: Start an Azure Data Factory pipeline run, poll it to a terminal state, read the
  per-activity detail, and cancel it safely if it needs to stop. Use when asked to trigger,
  monitor or abort an ADF pipeline.
api: microsoft-azure-data-factory
version: '2018-06-01'
operations:
  - Pipelines_ListByFactory
  - Pipelines_Get
  - Pipelines_CreateRun
  - PipelineRuns_Get
  - PipelineRuns_QueryByFactory
  - PipelineRuns_Cancel
  - ActivityRuns_QueryByPipelineRun
---

# Run an Azure Data Factory pipeline

Base URL `https://management.azure.com`. Every request needs `?api-version=2018-06-01` and an
`Authorization: Bearer <token>` header for audience `https://management.azure.com/`.

Throughout, `{scope}` means
`/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}`.

## Before you start

**This costs money and it is not replayable.** `Pipelines_CreateRun` accepts no idempotency key.
Calling it twice starts two runs and bills both. Record the `runId` it returns *before* you
consider any retry, and never retry blind on a timeout — query first (step 5), then decide.

## 1. Find the pipeline

```
GET {scope}/pipelines?api-version=2018-06-01
```

`Pipelines_ListByFactory`. Returns `{"value":[...],"nextLink":...}`. Follow `nextLink` verbatim if
present. To read one definition including its activity graph, use `Pipelines_Get`:

```
GET {scope}/pipelines/{pipelineName}?api-version=2018-06-01
```

## 2. Start the run

```
POST {scope}/pipelines/{pipelineName}/createRun?api-version=2018-06-01
Content-Type: application/json

{ "<parameterName>": "<value>" }
```

`Pipelines_CreateRun`. The body is the pipeline's parameter map. Useful query parameters:

- `referencePipelineRunId` — rerun an existing run
- `isRecovery` — recovery-mode rerun
- `startActivityName` — begin from a named activity
- `startFromFailure` — restart from the failed activity

The response is `{"runId": "<guid>"}`. **Persist that runId now.**

## 3. Poll the run

```
GET {scope}/pipelineruns/{runId}?api-version=2018-06-01
```

`PipelineRuns_Get`. Read `status`. Terminal values are `Succeeded`, `Failed` and `Cancelled`;
anything else (`Queued`, `InProgress`, `Cancelling`) means keep waiting. Back off between polls —
this is a subscription-scoped read against Azure Resource Manager's token bucket, and hammering it
throttles every other caller on the same subscription. Watch
`x-ms-ratelimit-remaining-subscription-reads` on each response and slow down before it reaches
zero.

On `Failed`, `message` carries the failure text and `runDimension`/`invokedBy` carry the context.

## 4. Read the per-activity detail

```
POST {scope}/pipelineruns/{runId}/queryActivityruns?api-version=2018-06-01

{ "lastUpdatedAfter": "<iso8601>", "lastUpdatedBefore": "<iso8601>" }
```

`ActivityRuns_QueryByPipelineRun`. This is where the real diagnosis lives: each entry carries
`activityName`, `activityType`, `status`, `error`, `input`, `output` and `durationInMs`. A pipeline
that failed tells you little; the failing activity tells you everything.

The response returns a `continuationToken` when there is more; resend the same body with
`continuationToken` set.

## 5. Find a run you lost

```
POST {scope}/queryPipelineRuns?api-version=2018-06-01

{ "lastUpdatedAfter": "<iso8601>", "lastUpdatedBefore": "<iso8601>",
  "filters": [ { "operand": "PipelineName", "operator": "Equals", "values": ["<pipelineName>"] } ] }
```

`PipelineRuns_QueryByFactory`. Use this instead of re-running when a `CreateRun` call timed out and
you do not know whether it landed.

## 6. Cancel

```
POST {scope}/pipelineruns/{runId}/cancel?api-version=2018-06-01
```

`PipelineRuns_Cancel`. Add `?isRecursive=true` to cancel child pipeline runs started by
`ExecutePipeline` activities as well.

This is the only reversal available on this flow, and it only works while the run is still in
flight. Microsoft states no time window for it; once the run reaches a terminal status it cannot
be cancelled and there is no undo for work it already performed on downstream stores. Whatever the
pipeline wrote, it wrote.

## Errors

| Status | Meaning | Do |
| --- | --- | --- |
| 400 `MissingApiVersionParameter` | You forgot `?api-version=` | Add it |
| 401 | Token missing or expired | Re-acquire from Entra ID |
| 403 | RBAC role missing | Assign Data Factory Contributor on the factory |
| 404 | Factory, pipeline or runId not found | Check the scope path |
| 429 | ARM throttling | Sleep `Retry-After` seconds, then retry |
| 5xx | Transient | Exponential backoff; keep `x-ms-request-id` for support |

Full catalog: `errors/microsoft-azure-data-factory-problem-types.yml`.
