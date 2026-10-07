---
name: cognite
description: Use when building data integration pipelines, querying industrial data, deploying data models, managing access control, or developing applications that connect to industrial assets, time series, events, and files. Reach for this skill when working with REST APIs, SDKs (Python/JavaScript), data modeling, extractors, transformations, or infrastructure-as-code deployments. Use for **Cognite Flows** custom web apps hosted in CDF (React, `@cognite/cli`, Aura design-system UI with `@cognite/aura`, app hosting, local dev with Vite, deploy, and certification). Core data modelling (CDM)—use when working with CogniteAsset, CogniteTimeSeries, CogniteFile—the CDM concepts for assets, time series, and files. Reach for this skill when building asset hierarchies, populating time series, creating and linking files, or when searching for "Asset" in the API reference (CDM assets are in the Instances API, not the legacy /assets endpoint).
metadata:
  mintlify-proj: cognite
  version: "1.0"
---

# Cognite Data Fusion (CDF) skill

## Product summary

Cognite Data Fusion is an industrial data platform that ingests, models, and exposes data from operational technology (OT) and information technology (IT) systems. Agents use CDF to build data pipelines (extract → transform → contextualize), define industrial knowledge graphs via data modeling, query resources via REST API or SDKs, and deploy configurations using the Cognite Toolkit. **Cognite Flows** adds a path to build and host **custom React applications** inside CDF (templates, CDF auth, AI-oriented skills, deploy); custom app UI uses the **Aura** design system (`@cognite/aura`). Key entry points: REST API at `https://{cluster}.cognitedata.com/api/v1`, Python SDK (`cognite-sdk`), JavaScript SDK (`@cognite/sdk`), the Cognite Toolkit CLI (`cdf`), and Flows via `@cognite/cli` apps. Primary docs: [docs.cognite.com](https://docs.cognite.com)

## API reference versioning

When linking to **conceptual** API reference pages (resource overviews, rate limits, introduction), use the **versioned URL path** that matches the calendar API version you mean. The published docs default to **`20230101`** unless the user or context specifies another calendar version (for example beta or alpha).

| Concept | Details |
| ------- | ------- |
| **Default calendar version in URLs** | `20230101` — use paths like `/api-reference/concepts/20230101/<page>` (for example [`/api-reference/concepts/20230101/api-description`](/api-reference/concepts/20230101/api-description)). |
| **Runtime API behavior** | Clients select behavior with the **`Cdf-Version`** HTTP header (`YYYYMMDD`, optional `-beta` / `-alpha` suffix). That is independent of which docs path you cite. |
| **Policy** | Deprecation, compatibility rules, and header semantics are documented in [API versions](/dev/API_versioning). |

If the user is browsing a **different** API spec version in the API reference UI, prefer links under the same calendar segment (for example `20230101-beta` or `20230101-alpha`) when those stub pages exist in the repo.

## When to use

Reach for this skill when:

- **Integrating data**: Setting up extractors (OPC UA, PI, SAP, databases) to stream data into CDF, configuring extraction pipelines, or monitoring data ingestion
- **Modeling data**: Designing data models with spaces, containers, views, and instances; querying graphs with GraphQL or REST; managing access via spaces
- **Working with Assets in CDM**: Creating or updating CogniteAsset hierarchies, populating assets via transformations, querying assets in CDF Search (shown as "Asset")
- **Working with Assets (legacy)**: Maintaining existing asset-centric applications using the `/assets` API
- **Querying resources**: Retrieving assets, time series, events, files, or sequences; using external IDs for lookups; filtering with advanced query language (AQL)
- **Deploying infrastructure**: Using the Cognite Toolkit to manage CDF projects as code, setting up CI/CD pipelines, or deploying modules
- **Building applications**: Authenticating with OAuth 2.0/OIDC, using Python/JavaScript SDKs to read/write data, or calling REST endpoints
- **Building Flows custom apps**: Creating React apps with `@cognite/cli`, using [Aura](/cdf/aura/index) components and tokens, running them locally (Vite), deploying to CDF app hosting, or meeting [builder certification](/cdf/flows/guides/builder-certification) and [quality guidelines](/cdf/flows/guides/quality-guidelines) for customer environments
- **Managing access**: Configuring OIDC providers, creating groups, assigning capabilities, or controlling access to spaces and data sets
- **Automating workflows**: Setting up data workflows with tasks and triggers, transforming data, or orchestrating multi-step processes

## Core data modeling vs. legacy

The Cognite Data Fusion (CDF) platform supports two modes:

| Mode                          | Use case                            | Key concepts                                 | API                                           |
| ----------------------------- | ----------------------------------- | -------------------------------------------- | --------------------------------------------- |
| **Core data modeling (CDM)** | New projects, knowledge graphs      | CogniteAsset, CogniteTimeSeries, CogniteFile | Instances API, GraphQL                        |
| **Legacy**                    | Existing asset-centric applications | Assets, Time series, Events, Files           | `/assets`, `/timeseries`, `/events`, `/files` |

For **new development**, prefer core data modeling. Use the legacy APIs **only** when maintaining existing applications.

## Quick reference

### Core resource types (core data modeling)

| Resource    | CDM concept           | Purpose                                               | API / SDK                                     |
| ----------- | --------------------- | ----------------------------------------------------- | --------------------------------------------- |
| Assets      | **CogniteAsset**      | Hierarchical entities; shown as "Asset" in CDF Search | Instances API / `data_modeling.instances`     |
| Time series | **CogniteTimeSeries** | Ordered data points over time                         | Instances API + Time Series API (data points) |
| Files       | **CogniteFile**       | Documents, diagrams, images                           | Instances API + File content API (upload)     |

### Legacy resource types

| Resource    | Legacy API    | Use when                                  |
| ----------- | ------------- | ----------------------------------------- |
| Assets      | `/assets`     | Maintaining existing asset-centric apps   |
| Time series | `/timeseries` | Metadata only; data points work with both |
| Events      | `/events`     | Legacy event storage                      |
| Files       | `/files`      | Metadata only; content works with both    |

### Other resource types

| Resource    | Purpose                               | Key field             |
| ----------- | ------------------------------------- | --------------------- |
| RAW         | Unstructured staging data             | `dbName`, `tableName` |
| Data models | Graphs with spaces, containers, views | `space`, `externalId` |

### Cognite Flows (custom web apps in CDF)

- **Overview** — [Building Flows custom applications](/cdf/flows/index): when to use Flows versus other surfaces (for example Streamlit or Cognite Functions).
- **First app** — [Get started with Flows custom apps](/cdf/flows/guides/getting-started): Node, `@cognite/cli`, create a project, run in CDF.
- **UI** — [Aura](/cdf/aura/index), [Install](/cdf/aura/guides/installation), [Primitives](/cdf/aura/primitives/index): design system for Flows custom app UI (`@cognite/aura`).
- **Concepts** — [Flows features](/cdf/flows/concepts/features), [App lifecycle](/cdf/flows/concepts/app-lifecycle): auth, Vite, skills, spec-driven workflow. For capabilities, see [Assign capabilities](/cdf/access/guides/capabilities#flows-custom-apps).
- **Ship** — [Run locally](/cdf/flows/guides/running-locally), [Deploy](/cdf/flows/guides/deploying): dev server and publishing to CDF.
- **Certification** — [Builder certification](/cdf/flows/guides/builder-certification), [Quality guidelines](/cdf/flows/guides/quality-guidelines): customer production requirements.
- **APIs in apps** — [Flows Auth API](/cdf/flows/reference/api/auth), [Vite plugin API](/cdf/flows/reference/api/vite): `connectToHostApp` and local tooling.

### Common developer goals

| Goal                                | CDM approach                                                  | Documentation                                                                                                    |
| ----------------------------------- | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **Build an asset hierarchy**        | Create CogniteAsset instances with `parent` via Instances API | [Building an asset hierarchy](/cdf/dm/dm_guides/dm_cdm_build_asset_hierarchy)                                    |
| **Create and populate time series** | Create CogniteTimeSeries; use Time Series API for data points | [Integrate time series](/cdf/dm/dm_guides/dm_integrate_with_time_series)                                         |
| **Create and link files**           | Create CogniteFile instances; use File content API for upload | [Integrate files](/cdf/dm/dm_guides/dm_integrate_files)                                                          |
| **Query assets**                    | Search/list CogniteAsset via Instances API or GraphQL         | [Core data model](/cdf/dm/dm_reference/dm_core_data_model#asset), [Instances](/api-reference/concepts/20230101/instances) |
| **Link time series to assets**      | Set `assets` relation on CogniteTimeSeries                    | [Integrate time series](/cdf/dm/dm_guides/dm_integrate_with_time_series)                                         |
| **Link files to assets**            | Set `assets` relation on CogniteFile                          | [Integrate files](/cdf/dm/dm_guides/dm_integrate_files)                                                          |

### Authentication patterns

| Scenario            | Method                            | Use case                     |
| ------------------- | --------------------------------- | ---------------------------- |
| Server-side scripts | API key or client credentials     | Extractors, scheduled jobs   |
| Web applications    | OAuth 2.0 bearer token            | Frontend apps, user sessions |
| Python SDK          | OIDC with Entra ID                | Interactive scripts, Jupyter |
| Cognite Toolkit     | Service principal + client secret | CI/CD, automated deployments |

### Cognite Toolkit workflow

```bash
cdf modules init                    # Initialize project structure
cdf build --env=dev                 # Build artifacts from YAML configs
cdf deploy --dry-run --env=dev      # Validate before deploying
cdf deploy --env=dev                # Deploy to CDF project
```

### Configuration files

- `cdf.toml` — Global CLI settings (organization, environment, plugins)
- `config.[env].yaml` — Per-environment project settings and module selection
- `modules/` — Resource directories (data_modeling/, raw/, access/, etc.)
- `*.yaml` — Resource configs (e.g., `my.space.yaml`, `my.container.yaml`)

### Common API endpoints

| Operation                 | CDM endpoint                                          | Legacy endpoint                    |
| ------------------------- | ----------------------------------------------------- | ---------------------------------- |
| Create/update assets      | `POST /datamodels/instances/query` (Instances API)    | `POST /assets`                     |
| Create/update time series | Instances API + `POST /timeseries/data` (data points) | `POST /timeseries`                 |
| Create/update files       | Instances API + `POST /files/uploadlink`              | `POST /files`                      |
| List/query assets         | Instances API, GraphQL                                | `GET /assets`, `POST /assets/list` |
| Query data model          | `POST /graphql`                                       | —                                  |

## Decision guidance

### When to use REST API vs SDK

| Condition                         | Use REST API | Use SDK |
| --------------------------------- | ------------ | ------- |
| Simple one-off requests           | ✓            |         |
| Batch operations, high throughput |              | ✓       |
| Complex data transformations      |              | ✓       |
| Scripting/automation              |              | ✓       |
| Direct HTTP integration           | ✓            |         |

### When to use RAW vs data modeling

| Scenario                         | RAW | Data modeling |
| -------------------------------- | --- | ------------- |
| Staging raw source data          | ✓   |               |
| Temporary transformation storage | ✓   |               |
| Structured industrial graphs     |     | ✓             |
| Long-term queryable data         |     | ✓             |
| Access control by space          |     | ✓             |

### When to use external ID vs internal ID

| Use case                      | External ID | Internal ID |
| ----------------------------- | ----------- | ----------- |
| Linking to source systems     | ✓           |             |
| Avoiding duplicates on insert | ✓           |             |
| Human-readable lookups        | ✓           |             |
| Performance-critical reads    |             | ✓           |
| Batch operations              | ✓           |             |

### Query approach: CRUD vs advanced query

| Need                          | CRUD endpoints | Advanced query (AQL) |
| ----------------------------- | -------------- | -------------------- |
| Fast, immediate consistency   | ✓              |                      |
| Batch read/write operations   | ✓              |                      |
| Complex filtering on metadata |                | ✓                    |
| Human exploration/analysis    |                | ✓                    |
| Large-scale synchronization   | ✓              |                      |

## Workflow

### 1. Set up authentication and project access

- Identify the authentication method (API key, OAuth 2.0, service principal)
- For Cognite Toolkit: configure `cdf.toml` with organization and environment
- For SDKs: set up OIDC provider (Entra ID or Amazon Cognito) and obtain credentials
- Test connectivity: `cdf status` or `client = CogniteClient()` in Python

### 2. Understand your data model

- Identify source systems and their data types (time series, events, assets)
- Map external IDs from source systems to CDF resources
- Decide: will you use RAW for staging, or ingest directly into data models?
- If using data modeling: design spaces, containers, and views for your domain

### 3. Extract and stage data

- Choose an extractor (OPC UA, PI, SAP, database, REST, file, etc.)
- Configure the extractor with source credentials and CDF connection
- Set up an extraction pipeline to monitor ingestion
- Verify data arrives in RAW or target data model

### 4. Transform and contextualize

- Write SQL transformations to reshape RAW data into CDF resource types
- Use entity matching to link entities across source systems
- Build relationships between assets, time series, and events
- Assign external IDs consistently across all resources

### 5. Query and expose data

- Use REST API or SDK to retrieve resources by external ID or filter
- For complex queries: use GraphQL on data models or advanced query language (AQL)
- Implement pagination for large result sets (max 10,000 per request)
- Cache results where appropriate to reduce API calls

### 6. Deploy with infrastructure-as-code

- Define all resources (spaces, containers, views, access groups) in YAML
- Organize configs in modules under `modules/` directory
- Use `cdf build` to validate and generate artifacts
- Use `cdf deploy --dry-run` to preview changes before applying
- Commit configs to version control and integrate with CI/CD (GitHub Actions, Azure DevOps, GitLab)

## Common gotchas

- **Asset search discovery**: Searching for "Asset" in the API reference surfaces legacy `/assets` endpoints. For Core Data Modeling, use the [Instances API](/api-reference/concepts/20230101/instances) with CogniteAsset—see [Core data model](/cdf/dm/dm_reference/dm_core_data_model#asset) and [Building an asset hierarchy](/cdf/dm/dm_guides/dm_cdm_build_asset_hierarchy).
- **External ID uniqueness**: External IDs are unique per resource type, not globally. An asset and time series can both have `externalId=123`. Enforce this in your source system mapping.
- **Search vs CRUD consistency**: Advanced query (AQL) is eventually consistent and slower than CRUD endpoints. Don't use it for large-scale batch synchronization; use `/byids` or `/list` instead.
- **Pagination limits**: Max 10,000 items per page. For data modeling queries, pagination only works at the top level; nested results cannot be paginated.
- **Data modeling access control**: Access is scoped to spaces, not data sets. Users need `dataModelsAcl.READ` to the space and `dataModelInstancesAcl.READ/WRITE` to instances.
- **Extraction pipeline monitoring**: Create extraction pipelines to track ingestion health. Without them, you won't see run history or failure notifications.
- **Toolkit module ordering**: Spaces must be created before containers, containers before views, and views before data models. Use numbered prefixes (e.g., `01_space.yaml`, `02_container.yaml`) if dependencies exist within the same type.
- **Token expiration**: OAuth 2.0 tokens expire. SDKs handle refresh automatically, but custom HTTP clients must implement token refresh logic.
- **Rate limiting**: CDF enforces throttling on parallel requests. Default: 20 parallel time series operations, 10 parallel data point operations. Respect these limits or requests will be queued.
- **Deprecated API versions**: API v0.5, v0.6 are removed. Always use the latest API version (v1).
- **Missing capabilities**: Users need specific capabilities (e.g., `timeseries:read`, `assets:write`) to perform operations. Check access errors against the capabilities reference.

## Verification checklist

Before submitting work:

- [ ] **Authentication works**: Test with `cdf status` (Toolkit) or `client.data_modeling.instances.list()` (SDK, CDM) or `client.assets.list()` (SDK, legacy)
- [ ] **External IDs are set**: All resources have unique, consistent external IDs from source systems
- [ ] **Data flows end-to-end**: Verify data appears in CDF (check extraction pipeline runs, query a sample asset/time series)
- [ ] **Access is configured**: Test that intended users/groups can read/write resources; check space and capability assignments
- [ ] **Queries are efficient**: For data modeling, run with `profile: true` to check debug notices; avoid full table scans
- [ ] **Pagination is handled**: If retrieving >10,000 items, implement cursor-based pagination
- [ ] **Dry-run passes**: Run `cdf deploy --dry-run` and review changes before applying
- [ ] **CI/CD is integrated**: Toolkit configs are in version control and CI/CD pipeline validates/deploys on merge
- [ ] **Monitoring is in place**: Extraction pipelines, data workflows, and functions have alerts configured
- [ ] **Documentation is updated**: Record external ID mappings, data model schema, and access policies

## Resources

### Core data modeling

- **Core data model reference**: [CogniteAsset, CogniteTimeSeries, CogniteFile](/cdf/dm/dm_reference/dm_core_data_model)
- **Build asset hierarchy**: [dm_cdm_build_asset_hierarchy](/cdf/dm/dm_guides/dm_cdm_build_asset_hierarchy)
- **Integrate time series**: [dm_integrate_with_time_series](/cdf/dm/dm_guides/dm_integrate_with_time_series)
- **Integrate files**: [dm_integrate_files](/cdf/dm/dm_guides/dm_integrate_files)
- **Instances API**: [Overview](/api-reference/concepts/20230101/instances)

### General

- **Cognite Flows**: [Overview](/cdf/flows/index) — [Get started](/cdf/flows/guides/getting-started) — [Deploy](/cdf/flows/guides/deploying) — [Flows features](/cdf/flows/concepts/features) — [Aura](/cdf/aura/index)
- **Comprehensive navigation**: [docs.cognite.com/llms.txt](https://docs.cognite.com/llms.txt) — Mintlify-generated index; follow `/_llms/` links recursively until you reach `.md` page URLs
- **REST API reference**: [/api-reference/concepts/20230101/api-description](/api-reference/concepts/20230101/api-description)
- **Python SDK**: [docs.cognite.com/dev/sdks/python](https://docs.cognite.com/dev/sdks/python/index)
- **JavaScript SDK**: [docs.cognite.com/dev/sdks/js](https://docs.cognite.com/dev/sdks/js/index)
- **Cognite Toolkit**: [docs.cognite.com/cdf/deploy/cdf_toolkit](https://docs.cognite.com/cdf/deploy/cdf_toolkit/index)
- **Data modeling**: [docs.cognite.com/cdf/dm](https://docs.cognite.com/cdf/dm/index)
- **Data integration**: [docs.cognite.com/cdf/integration](https://docs.cognite.com/cdf/integration/index)
- **Access control**: [docs.cognite.com/cdf/access](https://docs.cognite.com/cdf/access/index)

---

> For additional documentation and navigation, see: [docs.cognite.com/llms.txt](https://docs.cognite.com/llms.txt)