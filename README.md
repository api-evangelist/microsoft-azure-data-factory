# Azure Data Factory

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Azure Data Factory is Microsoft's cloud-based data integration service, orchestrating and automating the movement and transformation of data across ETL and ELT workloads that span cloud and on-premises stores. Its public interface is the Microsoft.DataFactory resource provider behind Azure Resource Manager: 104 operations over 75 paths at api-version 2018-06-01, covering factories, pipelines and pipeline runs, datasets, linked services, mapping data flows, triggers, integration runtimes, credentials, global parameters, managed virtual networks and private endpoints, and change data capture resources. Authentication is OAuth 2.0 against Microsoft Entra ID with a single delegated scope, and authorization is Azure RBAC role assignment rather than API scopes. The contract is notable for its type system: 1,199 schema definitions, of which 121 are linked-service connector subtypes and 105 are dataset subtypes, all resolved through OpenAPI discriminators.

**Areas:** Data Integration · ETL · ELT · Data Pipeline · Data Movement · Orchestration · Data Engineering · Change Data Capture · Integration Runtime · Cloud · Microsoft Azure · Data Factory

## Azure Data Factory on APIs.io

Everything profiled for Azure Data Factory is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/microsoft-azure-data-factory/](https://apis.io/providers/microsoft-azure-data-factory/)** — or go straight to one of the APIs or properties below.

### APIs (25)

- [Azure Data Factory Activityruns API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-activityruns-api/) — Activityruns operations on the Microsoft.DataFactory resource provider (1 operation): ActivityRuns_QueryByPipelineRun.
- [Azure Data Factory Credentials API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-credentials-api/) — Credentials operations on the Microsoft.DataFactory resource provider (4 operations): CredentialOperations_ListByFactory, CredentialOperations_Get,…
- [Azure Data Factory Datasets API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-datasets-api/) — Datasets operations on the Microsoft.DataFactory resource provider (4 operations): Datasets_ListByFactory, Datasets_Get, Datasets_CreateOrUpdate,…
- [Azure Data Factory Factories API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-factories-api/) — Factories operations on the Microsoft.DataFactory resource provider (9 operations): Factories_List, Factories_ConfigureFactoryRepo,…
- [Azure Data Factory Operations API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-operations-api/) — Operations operations on the Microsoft.DataFactory resource provider (1 operation): Operations_List.
- [Azure Data Factory Pipelineruns API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-pipelineruns-api/) — Pipelineruns operations on the Microsoft.DataFactory resource provider (3 operations): PipelineRuns_Get, PipelineRuns_Cancel, PipelineRuns_QueryByFactory.
- [Azure Data Factory Pipelines API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-pipelines-api/) — Pipelines operations on the Microsoft.DataFactory resource provider (5 operations): Pipelines_ListByFactory, Pipelines_Get, Pipelines_CreateOrUpdate,…
- [Azure Data Factory Trigger API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-trigger-api/) — Trigger operations on the Microsoft.DataFactory resource provider (1 operation): Triggers_Get.
- [Azure Data Factory Triggerruns API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-triggerruns-api/) — Triggerruns operations on the Microsoft.DataFactory resource provider (3 operations): TriggerRuns_QueryByFactory, TriggerRuns_Cancel, TriggerRuns_Rerun.
- [Azure Data Factory Triggers API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-triggers-api/) — Triggers operations on the Microsoft.DataFactory resource provider (9 operations): Triggers_QueryByFactory, Triggers_ListByFactory, Triggers_CreateOrUpdate,…
- [Azure Data Factory Change Data Capture API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-changedatacapture-api/) — The changeDataCapture API from Azure Data Factory — 5 operation(s) for changedatacapture.
- [Azure Data Factory Data Flow Debug Session API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-dataflowdebugsession-api/) — The dataFlowDebugSession API from Azure Data Factory — 5 operation(s) for dataflowdebugsession.
- [Azure Data Factory Data Flows API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-dataflows-api/) — The dataFlows API from Azure Data Factory — 2 operation(s) for dataflows.
- [Azure Data Factory Exposure Control API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-exposurecontrol-api/) — The exposureControl API from Azure Data Factory — 3 operation(s) for exposurecontrol.
- [Azure Data Factory Global Parameters API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-globalparameters-api/) — The globalParameters API from Azure Data Factory — 2 operation(s) for globalparameters.
- [Azure Data Factory Integration Runtime Disable Interactive Query API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimedisableinteractivequery-api/) — The integrationRuntimeDisableInteractiveQuery API from Azure Data Factory — 1 operation(s) for integrationruntimedisableinteractivequery.
- [Azure Data Factory Integration Runtime Enable Interactive Query API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimeenableinteractivequery-api/) — The integrationRuntimeEnableInteractiveQuery API from Azure Data Factory — 1 operation(s) for integrationruntimeenableinteractivequery.
- [Azure Data Factory Integration Runtime Nodes API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimenodes-api/) — The integrationRuntimeNodes API from Azure Data Factory — 2 operation(s) for integrationruntimenodes.
- [Azure Data Factory Integration Runtime Object Metadata API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimeobjectmetadata-api/) — The integrationRuntimeObjectMetadata API from Azure Data Factory — 2 operation(s) for integrationruntimeobjectmetadata.
- [Azure Data Factory Integration Runtimes API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimes-api/) — The integrationRuntimes API from Azure Data Factory — 14 operation(s) for integrationruntimes.
- [Azure Data Factory Linked Services API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-linkedservices-api/) — The linkedServices API from Azure Data Factory — 2 operation(s) for linkedservices.
- [Azure Data Factory Managed Private Endpoints API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-managedprivateendpoints-api/) — The managedPrivateEndpoints API from Azure Data Factory — 2 operation(s) for managedprivateendpoints.
- [Azure Data Factory Managed Virtual Networks API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-managedvirtualnetworks-api/) — The managedVirtualNetworks API from Azure Data Factory — 2 operation(s) for managedvirtualnetworks.
- [Azure Data Factory Private End Point Connections API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-privateendpointconnections-api/) — The privateEndPointConnections API from Azure Data Factory — 2 operation(s) for privateendpointconnections.
- [Azure Data Factory Private Link Resources API](https://apis.io/apis/microsoft-azure-data-factory/microsoft-azure-data-factory-privatelinkresources-api/) — The privateLinkResources API from Azure Data Factory — 1 operation(s) for privatelinkresources.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [microsoft-azure-data-factory-mcp.yml](https://apis.io/servers/microsoft-azure-data-factory/microsoft-azure-data-factory-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Microsoft Azure Data Factory Agentic Access](https://apis.io/agentic-access/microsoft-azure-data-factory/microsoft-azure-data-factory-agentic-access/)

#### Examples (112)

Example requests and responses.

- [Microsoft Azure Data Factory Activityruns_Querybypipelinerun](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ActivityRuns_QueryByPipelineRun/)
- [Microsoft Azure Data Factory Approverejectprivateendpointconnection](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ApproveRejectPrivateEndpointConnection/)
- [Microsoft Azure Data Factory Changedatacapture_Create](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Create/)
- [Microsoft Azure Data Factory Changedatacapture_Delete](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Delete/)
- [Microsoft Azure Data Factory Changedatacapture_Get](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Get/)
- [Microsoft Azure Data Factory Changedatacapture_Listbyfactory](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_ListByFactory/)
- [Microsoft Azure Data Factory Changedatacapture_Start](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Start/)
- [Microsoft Azure Data Factory Changedatacapture_Status](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Status/)
- [Microsoft Azure Data Factory Changedatacapture_Stop](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Stop/)
- [Microsoft Azure Data Factory Changedatacapture_Update](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-ChangeDataCapture_Update/)
- [Microsoft Azure Data Factory Credentials_Create](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-Credentials_Create/)
- [Microsoft Azure Data Factory Credentials_Delete](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-Credentials_Delete/)
- [Microsoft Azure Data Factory Credentials_Get](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-Credentials_Get/)
- [Microsoft Azure Data Factory Credentials_Listbyfactory](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-Credentials_ListByFactory/)
- [Microsoft Azure Data Factory Dataflowdebugsession_Adddataflow](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlowDebugSession_AddDataFlow/)
- [Microsoft Azure Data Factory Dataflowdebugsession_Create](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlowDebugSession_Create/)
- [Microsoft Azure Data Factory Dataflowdebugsession_Delete](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlowDebugSession_Delete/)
- [Microsoft Azure Data Factory Dataflowdebugsession_Executecommand](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlowDebugSession_ExecuteCommand/)
- [Microsoft Azure Data Factory Dataflowdebugsession_Querybyfactory](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlowDebugSession_QueryByFactory/)
- [Microsoft Azure Data Factory Dataflows_Create](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlows_Create/)
- [Microsoft Azure Data Factory Dataflows_Delete](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlows_Delete/)
- [Microsoft Azure Data Factory Dataflows_Get](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlows_Get/)
- [Microsoft Azure Data Factory Dataflows_Listbyfactory](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlows_ListByFactory/)
- [Microsoft Azure Data Factory Dataflows_Update](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-DataFlows_Update/)
- [Microsoft Azure Data Factory Datasets_Create](https://apis.io/examples/microsoft-azure-data-factory/microsoft-azure-data-factory-Datasets_Create/)
- …and 87 more published on APIs.io

#### Collections (3)

Postman and Open Collection request collections.

- [Azure Data Factory REST API](https://apis.io/collections/microsoft-azure-data-factory/open-microsoft-azure-data-factory/)
- [Azure Data Factory REST Factories API](https://apis.io/collections/microsoft-azure-data-factory/open-microsoft-azure-data-factory-factories-api/)
- [Azure Data Factory REST Factories Operations API](https://apis.io/collections/microsoft-azure-data-factory/open-microsoft-azure-data-factory-operations-api/)

#### Overlays (50)

OpenAPI overlays, including conversational phrasing for each operation.

- [Microsoft Azure Data Factory Activityruns Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-activityruns-api-overlay/)
- [Microsoft Azure Data Factory Activityruns Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-activityruns-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Change Data Capture Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-change-data-capture-api-overlay/)
- [Microsoft Azure Data Factory Changedatacapture Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-changedatacapture-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Credentials Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-credentials-api-overlay/)
- [Microsoft Azure Data Factory Credentials Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-credentials-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Data Flow Debug Session Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-data-flow-debug-session-api-overlay/)
- [Microsoft Azure Data Factory Data Flows Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-data-flows-api-overlay/)
- [Microsoft Azure Data Factory Dataflowdebugsession Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-dataflowdebugsession-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Dataflows Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-dataflows-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Datasets Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-datasets-api-overlay/)
- [Microsoft Azure Data Factory Datasets Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-datasets-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Exposure Control Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-exposure-control-api-overlay/)
- [Microsoft Azure Data Factory Exposurecontrol Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-exposurecontrol-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Factories Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-factories-api-overlay/)
- [Microsoft Azure Data Factory Factories Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-factories-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Global Parameters Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-global-parameters-api-overlay/)
- [Microsoft Azure Data Factory Globalparameters Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-globalparameters-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Integration Runtime Disable Interactive Query Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integration-runtime-disable-interactive-query-api-overlay/)
- [Microsoft Azure Data Factory Integration Runtime Enable Interactive Query Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integration-runtime-enable-interactive-query-api-overlay/)
- [Microsoft Azure Data Factory Integration Runtime Nodes Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integration-runtime-nodes-api-overlay/)
- [Microsoft Azure Data Factory Integration Runtime Object Metadata Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integration-runtime-object-metadata-api-overlay/)
- [Microsoft Azure Data Factory Integration Runtimes Api Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integration-runtimes-api-overlay/)
- [Microsoft Azure Data Factory Integrationruntimedisableinteractivequery Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimedisableinteractivequery-api-phrasing-overlay/)
- [Microsoft Azure Data Factory Integrationruntimeenableinteractivequery Api Phrasing Overlay](https://apis.io/overlays/microsoft-azure-data-factory/microsoft-azure-data-factory-integrationruntimeenableinteractivequery-api-phrasing-overlay/)
- …and 25 more published on APIs.io

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Microsoft Azure Data Factory Authentication](https://apis.io/security/microsoft-azure-data-factory/microsoft-azure-data-factory-authentication/)
- [Microsoft Azure Data Factory Domain Security](https://apis.io/security/microsoft-azure-data-factory/microsoft-azure-data-factory-domain-security/)
- [Microsoft Azure Data Factory Trust Center](https://apis.io/security/microsoft-azure-data-factory/microsoft-azure-data-factory-trust-center/)
- [Microsoft Azure Data Factory Vulnerability Disclosure](https://apis.io/security/microsoft-azure-data-factory/microsoft-azure-data-factory-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Microsoft Azure Data Factory Scopes](https://apis.io/scopes/microsoft-azure-data-factory/microsoft-azure-data-factory-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Microsoft Azure Data Factory Plans Pricing](https://apis.io/plans/microsoft-azure-data-factory/microsoft-azure-data-factory-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Microsoft Azure Data Factory Rate Limits](https://apis.io/rate-limits/microsoft-azure-data-factory/microsoft-azure-data-factory-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Microsoft Azure Data Factory Finops](https://apis.io/finops/microsoft-azure-data-factory/microsoft-azure-data-factory-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.microsoft.com/)
- [Documentation](https://learn.microsoft.com/en-us/azure/data-factory/)
- [Getting started](https://learn.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory-rest-api)
- [API reference](https://learn.microsoft.com/en-us/rest/api/datafactory/)
- [Pricing](https://azure.microsoft.com/en-us/pricing/details/data-factory/data-pipeline/)
- [Sign up](https://signup.azure.com/)
- [Support](https://support.microsoft.com/)
- [Changelog](https://learn.microsoft.com/en-us/azure/data-factory/whats-new)
- [Blog](https://techcommunity.microsoft.com/category/analytics/blog/azuredatafactoryblog)
- [Terms of service](https://www.microsoft.com/en-us/legal/terms-of-use)
- [Privacy policy](https://privacy.microsoft.com/en-us/privacystatement)
- [GitHub](https://github.com/Azure)
- [Status](https://azure.status.microsoft/en-us/status)

## API Evangelist rating

**Kin Score 70.5** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 73.2 |
| Contract quality | 46.0 |
| Contract governance | 18.2 |
| Operational transparency | 89.5 |
| Developer ergonomics | 80.4 |
| Access clarity | 78.9 |

**Agent readiness 35.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 45.1** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/microsoft-azure-data-factory/](https://apis.io/providers/microsoft-azure-data-factory/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Azure Data Factory: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/microsoft-azure-data-factory/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
