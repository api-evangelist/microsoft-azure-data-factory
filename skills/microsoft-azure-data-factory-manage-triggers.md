---
name: microsoft-azure-data-factory-manage-triggers
description: Create, start, stop and inspect Azure Data Factory triggers, including event-trigger
  subscription to Event Grid, and rerun or cancel individual trigger instances. Use when asked to
  schedule ADF pipelines or to stop a trigger that is firing.
api: microsoft-azure-data-factory
version: '2018-06-01'
operations:
  - Triggers_CreateOrUpdate
  - Triggers_Get
  - Triggers_ListByFactory
  - Triggers_QueryByFactory
  - Triggers_Delete
  - Triggers_Start
  - Triggers_Stop
  - Triggers_SubscribeToEvents
  - Triggers_UnsubscribeFromEvents
  - Triggers_GetEventSubscriptionStatus
  - TriggerRuns_QueryByFactory
  - TriggerRuns_Cancel
  - TriggerRuns_Rerun
---

# Manage Azure Data Factory triggers

`{scope}` =
`/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}`,
`?api-version=2018-06-01` on every call.

## A created trigger is not a running trigger

`Triggers_CreateOrUpdate` writes the definition in a **Stopped** state. Nothing fires until you
call `Triggers_Start`. This trips up most first integrations.

```
PUT {scope}/triggers/{triggerName}?api-version=2018-06-01
if-match: <etag from Triggers_Get>

{ "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": { "recurrence": { "frequency": "Hour", "interval": 1,
                                        "startTime": "<iso8601>", "timeZone": "UTC" } },
    "pipelines": [ { "pipelineReference": { "type": "PipelineReference",
                                            "referenceName": "<pipelineName>" },
                     "parameters": { } } ]
} }
```

Four trigger subtypes exist: `ScheduleTrigger`, `TumblingWindowTrigger`, `BlobEventsTrigger` and
`CustomEventsTrigger`. Like everything in this API, the subtype is chosen by the `type`
discriminator.

## Start and stop

```
POST {scope}/triggers/{triggerName}/start?api-version=2018-06-01
POST {scope}/triggers/{triggerName}/stop?api-version=2018-06-01
```

Both are long-running operations: they can return 202, in which case poll the
`Azure-AsyncOperation` header URL (falling back to `Location`) honouring `Retry-After`, until the
returned `status` is `Succeeded`, `Failed` or `Canceled`.

`Triggers_Stop` is the clean reversal of `Triggers_Start` and works at any time. It halts **future**
firings only — pipeline runs the trigger already started keep going. To stop those too, cancel each
one with `PipelineRuns_Cancel`.

## Event triggers need a second step

`BlobEventsTrigger` and `CustomEventsTrigger` listen to Azure Event Grid. Writing the trigger is
not enough — you must subscribe it:

```
POST {scope}/triggers/{triggerName}/subscribeToEvents?api-version=2018-06-01
```

`Triggers_SubscribeToEvents` is long-running (202). Poll
`Triggers_GetEventSubscriptionStatus` until `status` reads `Enabled`. The reversal is
`Triggers_UnsubscribeFromEvents`, also long-running.

Note the direction of the relationship: Data Factory **consumes** Event Grid events here. It does
not publish events of its own, and it is not an Event Grid system-topic source, so there is no
outbound webhook or event catalog to subscribe to on the other side.

## Inspect what fired

```
POST {scope}/queryTriggerRuns?api-version=2018-06-01

{ "lastUpdatedAfter": "<iso8601>", "lastUpdatedBefore": "<iso8601>",
  "filters": [ { "operand": "TriggerName", "operator": "Equals", "values": ["<triggerName>"] } ] }
```

`TriggerRuns_QueryByFactory`. Paginate with the returned `continuationToken`.

Per instance:

- `TriggerRuns_Cancel` — `POST {scope}/triggers/{triggerName}/triggerRuns/{runId}/cancel`
- `TriggerRuns_Rerun` — `POST {scope}/triggers/{triggerName}/triggerRuns/{runId}/rerun`

`Rerun` starts real work and bills for it. Like `Pipelines_CreateRun` it carries no idempotency
key, so calling it twice reruns twice.

## Deleting

`Triggers_Delete` is final — no restore. Stop the trigger first so nothing fires mid-delete, and
confirm the factory is Git-backed if you might want the definition again.
