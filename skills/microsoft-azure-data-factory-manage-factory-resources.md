---
name: microsoft-azure-data-factory-manage-factory-resources
description: Create, read, update and delete the declarative objects inside an Azure Data Factory
  — pipelines, datasets, linked services and data flows — using ETag conditional writes so a
  concurrent editor is never silently overwritten. Use when asked to author or change ADF
  definitions through the API.
api: microsoft-azure-data-factory
version: '2018-06-01'
operations:
  - Factories_CreateOrUpdate
  - Factories_Get
  - Factories_List
  - LinkedServices_CreateOrUpdate
  - LinkedServices_Get
  - LinkedServices_ListByFactory
  - LinkedServices_Delete
  - Datasets_CreateOrUpdate
  - Datasets_Get
  - Datasets_ListByFactory
  - Datasets_Delete
  - Pipelines_CreateOrUpdate
  - Pipelines_Get
  - Pipelines_ListByFactory
  - Pipelines_Delete
  - DataFlows_CreateOrUpdate
  - DataFlows_Get
  - DataFlows_ListByFactory
  - DataFlows_Delete
---

# Manage Azure Data Factory resources

`{scope}` =
`/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataFactory/factories/{factoryName}`.
Every call carries `?api-version=2018-06-01` and a bearer token for
`https://management.azure.com/`.

## Build order matters

Data Factory objects reference each other by name. Create them in dependency order or the write
fails:

1. **Linked service** — the connection (`LinkedServices_CreateOrUpdate`)
2. **Dataset** — the shape at that connection, referencing the linked service
   (`Datasets_CreateOrUpdate`)
3. **Data flow** — optional transformation, referencing datasets (`DataFlows_CreateOrUpdate`)
4. **Pipeline** — the activity graph, referencing datasets and data flows
   (`Pipelines_CreateOrUpdate`)

Delete in the reverse order.

## Everything is a discriminated type

This is the one thing that makes ADF request bodies look impenetrable and then trivial. There is
no free-form config blob. Each object declares a `type` and the server validates against that
subtype — 121 linked-service subtypes, 105 dataset subtypes, 46 copy sinks, 40 copy sources.

```
PUT {scope}/linkedservices/{linkedServiceName}?api-version=2018-06-01

{ "properties": {
    "type": "AzureBlobStorage",
    "typeProperties": { "connectionString": "..." },
    "connectVia": { "type": "IntegrationRuntimeReference", "referenceName": "AutoResolveIntegrationRuntime" }
} }
```

Cross-object links are never bare strings either. They are reference objects:

```
{ "type": "LinkedServiceReference", "referenceName": "MyBlobStore", "parameters": { } }
```

The full hierarchy and the 23 reference types are enumerated in
`data-model/microsoft-azure-data-factory-data-model.yml`. Never put a secret inline — use
`AzureKeyVaultSecretReference`.

## Write conditionally. Always.

Twelve CreateOrUpdate operations accept an ETag:

```
GET {scope}/pipelines/{pipelineName}?api-version=2018-06-01
-> body carries "etag": "<value>"

PUT {scope}/pipelines/{pipelineName}?api-version=2018-06-01
if-match: <value>
```

If someone changed the object since your GET, the PUT returns **412 Precondition Failed** and
writes nothing. Re-read, merge onto the current version, resend. Sending `if-match: *` means
unconditional — do that only when you genuinely intend last-write-wins.

Omitting `if-match` entirely also means last-write-wins. In a factory that a human is editing in
Azure Data Factory Studio at the same time, that is how an agent silently destroys someone's work.

The conditional GET counterpart is `if-none-match`, which returns **304 Not Modified** and no body
when your cached ETag is still current — the cheap way to poll for change.

## Reading

```
GET {scope}/pipelines?api-version=2018-06-01
```

`{"value":[...],"nextLink":"<absolute url>"}`. Follow `nextLink` verbatim until it is absent.
There is no page-size, offset or cursor parameter to set, and no `$select` or `$expand` — objects
come back whole.

## Deleting is final

`Pipelines_Delete`, `Datasets_Delete`, `LinkedServices_Delete`, `DataFlows_Delete` and every other
delete in this API are one-way. The contract exposes **no undelete, restore or soft-delete
operation for any resource type**. A 204 means the object was already gone and is a success, not
an error.

The only recovery is source control: a factory configured with Git integration
(`Factories_ConfigureFactoryRepo`) can have its definitions redeployed from the repo. That is a
source-control action outside this API, not a reversal of your call. Confirm a factory is
Git-backed before you delete anything you might want back.

## Errors

412 means you lost an ETag race — re-read and merge. 403 means the RBAC role assignment is
missing, not that the token is wrong. 400 usually means the discriminated `type` value or its
`typeProperties` did not validate. Full catalog:
`errors/microsoft-azure-data-factory-problem-types.yml`.
