---
name: microsoft-azure-data-factory-manage-integration-runtimes
description: Provision, start, stop, monitor and key-rotate Azure Data Factory integration
  runtimes — the compute that actually moves data — including self-hosted node management. Use
  when asked about ADF compute, self-hosted IR health, or IR auth keys.
api: microsoft-azure-data-factory
version: '2018-06-01'
operations:
  - IntegrationRuntimes_CreateOrUpdate
  - IntegrationRuntimes_Get
  - IntegrationRuntimes_ListByFactory
  - IntegrationRuntimes_GetStatus
  - IntegrationRuntimes_Start
  - IntegrationRuntimes_Stop
  - IntegrationRuntimes_Upgrade
  - IntegrationRuntimes_SyncCredentials
  - IntegrationRuntimes_ListAuthKeys
  - IntegrationRuntimes_RegenerateAuthKey
  - IntegrationRuntimes_GetConnectionInfo
  - IntegrationRuntimes_GetMonitoringData
  - IntegrationRuntimes_ListOutboundNetworkDependenciesEndpoints
  - IntegrationRuntimes_CreateLinkedIntegrationRuntime
  - IntegrationRuntimes_RemoveLinks
  - IntegrationRuntimes_Delete
  - IntegrationRuntimeNodes_Get
  - IntegrationRuntimeNodes_Update
  - IntegrationRuntimeNodes_Delete
  - IntegrationRuntimeNodes_GetIpAddress
---

# Manage Azure Data Factory integration runtimes

`{scope}` =
`/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}`,
`?api-version=2018-06-01` on every call.

The integration runtime is the compute that actually executes an activity. It is the single
largest surface in this API — 17 of the 104 operations — and the one most likely to be the real
answer when a pipeline "just hangs".

## List and inspect

```
GET  {scope}/integrationRuntimes?api-version=2018-06-01
GET  {scope}/integrationRuntimes/{integrationRuntimeName}?api-version=2018-06-01
POST {scope}/integrationRuntimes/{integrationRuntimeName}/getStatus?api-version=2018-06-01
```

`IntegrationRuntimes_GetStatus` is a **POST**, not a GET, and it is the one that matters: it
returns the runtime's state plus per-node health for a self-hosted runtime. `Get` returns only the
definition.

For throughput and queue telemetry use `IntegrationRuntimes_GetMonitoringData`.

## Two subtypes, different lifecycles

- **Managed** (`type: "Managed"`) — Azure-hosted. `IntegrationRuntimes_Start` and
  `IntegrationRuntimes_Stop` apply to ManagedReserved runtimes and are long-running operations:
  they return 202, so poll `Azure-AsyncOperation` (or `Location`) honouring `Retry-After` until
  the status is terminal. Starting an SSIS integration runtime takes minutes and bills per VM-hour
  the entire time it is running — stop it when idle.
- **SelfHosted** (`type: "SelfHosted"`) — runs on customer machines. It is registered with an auth
  key, not started through this API.

## Self-hosted nodes

```
GET    {scope}/integrationRuntimes/{name}/nodes/{nodeName}?api-version=2018-06-01
PATCH  {scope}/integrationRuntimes/{name}/nodes/{nodeName}?api-version=2018-06-01
DELETE {scope}/integrationRuntimes/{name}/nodes/{nodeName}?api-version=2018-06-01
POST   {scope}/integrationRuntimes/{name}/nodes/{nodeName}/ipAddress?api-version=2018-06-01
```

`IntegrationRuntimeNodes_Update` sets `concurrentJobsLimit`. `IntegrationRuntimeNodes_Delete`
removes a node from the runtime; the machine itself is untouched.

`IntegrationRuntimes_Upgrade` triggers a self-hosted upgrade to the latest version.

## Auth keys — handle with care

```
POST {scope}/integrationRuntimes/{name}/listAuthKeys?api-version=2018-06-01
POST {scope}/integrationRuntimes/{name}/regenerateAuthKey?api-version=2018-06-01
     { "keyName": "authKey1" }
```

`ListAuthKeys` returns live registration secrets. Treat the response as a credential: never log
it, never echo it into a transcript, never persist it outside a secret store.

`RegenerateAuthKey` is **irreversible**. The moment it returns, the previous key value is gone and
every node still holding it loses registration. Rotate one key at a time (`authKey1`, then
`authKey2`) so nodes can migrate, and re-register nodes before rotating the second.

`IntegrationRuntimes_SyncCredentials` forces credential sync across nodes, overwriting every worker
node with the dispatcher's copy. Microsoft's own guidance in the contract says to prefer manually
importing the latest credential backup file over calling this API.

## Linked integration runtimes

`IntegrationRuntimes_CreateLinkedIntegrationRuntime` shares a self-hosted runtime with another
factory. Its reversal is `IntegrationRuntimes_RemoveLinks`, which removes all linked runtimes for
a given factory. There is no per-link removal operation.

## Networking

`IntegrationRuntimes_ListOutboundNetworkDependenciesEndpoints` returns the endpoints a self-hosted
runtime must reach — the first thing to check when a self-hosted node reports as unavailable
behind a firewall. `IntegrationRuntimes_GetConnectionInfo` returns the on-premises connection info
used for encrypting data-source credentials.

## Deleting

`IntegrationRuntimes_Delete` is final and there is no restore. Any pipeline whose activities bind
to that runtime will fail on the next run. Check `IntegrationRuntimes_GetStatus` and the linked
services that name it via `connectVia` before deleting.
