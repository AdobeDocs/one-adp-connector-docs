---
title: Adobe for Developers Connector tool reference
description: Reference for all tools available through the Adobe for Developers Connector plugin.
---

# Adobe for Developers Connector tool reference

The Adobe for Developers Connector provides tools for searching Adobe developer documentation, managing Developer Console resources, and configuring Adobe I/O Events. The tools shown here are registered by the connector. Results and available actions depend on the signed-in user and the organizations and permissions available to that account.

Most Developer Console resource operations require the Adobe Developer Terms to be accepted for the selected organization. Review the terms before accepting. Tools marked as modifying or removing resources request user approval in supported clients; review each change before approving.

## Adobe account and organization

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Organisations (`get_organisations`)

Get all Adobe organisations the authenticated user has access to.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

This tool does not require any parameters.

**Example prompt:**

* "Which Adobe organizations can I access?"

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Adobe User Profile (`get_adobe_user_profile`)

Returns the profile for the authenticated Adobe user.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

This tool does not require any parameters.

**Example prompt:**

* "Show the Adobe account profile I am signed in with."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Accept Developer Terms (`accept_developer_terms`)

Accept the Adobe Developer Terms of Service for an organisation. Call this after the user has reviewed the terms and confirmed they agree. Required before using most other tools that create or manage Console resources.

**Operation:** Accepts terms for an organization; call only after the user has reviewed and explicitly agreed.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |

**Example prompt:**

* "I have reviewed and agree to the Adobe Developer Terms for organization [orgId]."

## Documentation search

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Doc Collections (`list_doc_collections`)

List all available Adobe documentation collections (products/knowledge bases) that search_adobe_docs can be scoped to. Call this when the user wants to scope their search to a specific Adobe product (e.g. 'search only App Builder docs') or when a broad search_adobe_docs call returns nothing useful and narrowing might help. Returns collection IDs to pass to search_adobe_docs.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

This tool does not require any parameters.

**Example prompt:**

* "Which Adobe documentation collections are available?"

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Search Adobe Docs (`search_adobe_docs`)

Retrieves relevant passages from official Adobe developer documentation, ranked by relevance score — synthesis happens in your LLM, not here. ALWAYS call this tool in two situations: (1) Before answering any question about Adobe developer products, APIs, SDKs, or platform concepts — do not rely on training knowledge alone. (2) Proactively before starting provisioning flows such as creating credentials, subscribing to Adobe APIs, or setting up I/O Events — fetch context first so your guidance is grounded in official Adobe docs. Covers App Builder, Adobe I/O Events, Express Add-ons, Adobe Developer Console, IMS authentication, product profiles, API credentials, Runtime actions, and all other Adobe developer platform topics. Omit collectionId to search across all collections (default); call list_doc_collections first only if you need to scope to one product. Returns up to 10 passages with content, title, source URL, and relevance score — synthesize the answer from these and cite sources. If no results come back, try rephrasing or broadening the query before giving up.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `query` | Yes | String | The question or topic to search Adobe developer documentation for. |
| `numberOfResults` | No | Integer | Number of document chunks to return (1–10). Defaults to 5. Range: at least 1 and at most 10. |
| `collectionId` | No | String | Optional collection ID to scope the search. Call list_doc_collections first to get valid IDs. Omit to search all collections. |

**Example prompt:**

* "Search Adobe developer documentation for [topic]."

## Developer Console

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Projects (`get_projects`)

Get projects in an Adobe organisation. Use filterBy 'all' for every project or 'me' to show only projects you created or last modified.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `filterBy` | No | String (enum) | Filter projects: 'all' returns every project in the org, 'me' returns only projects where you are the creator or last modifier. Defaults to 'all'. Allowed values: `all`, `me`. |

**Example prompt:**

* "List all projects in organization [orgId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create Project (`create_project`)

Create a new project in an Adobe organisation. Use projectType 'default' for a standard project or 'appBuilder' for an App Builder project. Additional constraint: For `projectType: appBuilder`, include `templateId`.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `name` | Yes | String | Alphanumeric project name (no spaces). Pattern: `^[a-zA-Z0-9]+$`. |
| `title` | Yes | String | Human-readable project title. |
| `description` | No | String | Optional project description. |
| `projectType` | Yes | String (enum) | Project type: 'default' for a standard project, 'appBuilder' for an App Builder project. Allowed values: `default`, `appBuilder`. |
| `whoCreated` | No | String | Optional identifier of who created the project. |
| `templateId` | No | String | Optional template ID. Required when projectType is 'appBuilder'. |

**Example prompt:**

* "Create a project named [name] in organization [orgId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Edit Project (`edit_project`)

Edit an existing project's name, title, description, or notification settings. Either (name AND title) or notificationsEnabled must be provided. Changes are saved with no automatic undo; review them before approving. Additional constraint: Provide both `name` and `title`, or provide `notificationsEnabled`.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `name` | No | String | New project name (alphanumeric only). |
| `title` | No | String | New human-readable project title. |
| `description` | No | String | New project description. |
| `notificationsEnabled` | No | Boolean | Whether to enable project notifications. |

**Example prompt:**

* "Update project [projectId] in organization [orgId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Delete Project (`delete_project`)

Delete a project from an organisation. This is permanent and cannot be undone.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID to delete (the 'id' field from get_projects). |

**Example prompt:**

* "Delete project [projectId] from organization [orgId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Workspaces (`list_workspaces`)

List all workspaces in a project.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |

**Example prompt:**

* "List the workspaces in project [projectId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Workspace (`get_workspace`)

Get details of a specific workspace within a project.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID. |

**Example prompt:**

* "Show details for workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Delete Workspace (`delete_workspace`)

Delete a workspace from a project. This is permanent and cannot be undone.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID to delete (the 'id' field from list_workspaces). |

**Example prompt:**

* "Delete workspace [workspaceId] from project [projectId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Services (`list_services`)

List Adobe services available to an organisation. Optionally filter by SDK codes.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `sdkCodes` | No | String | Optional comma-separated list of SDK codes to filter results (e.g. 'AdobeAnalyticsSDK,CampaignSDK'). |
| `filterBy` | No | String (enum) | Filter services: 'all' returns every service, 'enabled' returns only services already available to the organisation. Defaults to 'all'. Allowed values: `all`, `enabled`. |

**Example prompt:**

* "List the Adobe services available to organization [orgId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Credentials (`get_credentials`)

Get all credentials for a workspace.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces or get_workspace). |

**Example prompt:**

* "List credentials in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Credential Secrets (`get_credential_secrets`)

Get a link to view a credential's client secrets in Adobe Developer Console. Secrets are never returned directly — always display the returned console_url as a clickable link: 🔗 View in Adobe Developer Console: &#123;console_url&#125;

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects or create_project). |
| `credentialId` | Yes | String | The credential ID (the 'id' field from get_credentials or any create credential response). |
| `credentialType` | Yes | String (enum) | The credential type, used to build the Console deep-link. Allowed values: `oauth_server_to_server`, `entp`, `adobeid`, `analytics`, `admin_entp`. |

**Example prompt:**

* "Show me the Developer Console link to view credential [credentialId] secrets."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Workspace Apis (`list_workspace_apis`)

List all APIs (services) subscribed to each credential in a workspace. Returns a grouped view: for each credential, shows which Adobe APIs are currently enabled.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces or get_workspace). |

**Example prompt:**

* "List the APIs subscribed to credentials in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Credential Services (`get_credential_services`)

Get all Adobe services (APIs) subscribed to a specific credential. Returns service names, SDK codes, scopes, roles, and license configs. Use this to inspect what APIs a credential currently has access to.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `credentialId` | Yes | String | The credential ID (the 'id' field from get_credentials or any create credential response). Also called the integration ID. |

**Example prompt:**

* "Show the APIs subscribed to credential [credentialId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create OAuth S2S Credential (`create_oauth_s2s_credential`)

Create an OAuth Server-to-Server credential in a specific workspace. Optionally subscribe services to it in the same call.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `name` | Yes | String | Name for the credential. |
| `description` | Yes | String | Description for the credential. |
| `templateId` | No | String | Optional template ID. |
| `includeSecret` | No | Boolean | Whether to include the client secret in the response. |
| `services` | No | Array of objects | Optional list of services to subscribe this credential to immediately. Item fields: `sdkCode` (String; required): The SDK code of the service to subscribe (e.g. 'AdobeAnalyticsSDK').; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Create an OAuth Server-to-Server credential named [name] in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create User Auth Credential (`create_user_auth_credential`)

Create an AdobeId (user OAuth) credential for a workspace. Use this for web apps, SPAs, native apps, or API key access. Additional constraint: For `WebApp`, `SinglePageApp`, or `Web`, provide `defaultRedirectUri` and a non-empty `redirectUriList`. For iOS or Android, provide `urlScheme`.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `name` | Yes | String | Name for the credential. |
| `description` | Yes | String | Description for the credential. |
| `platform` | Yes | String (enum) | Platform type: 'WebApp'/'Web' for web apps (needs redirect URI), 'SinglePageApp' for SPAs (needs redirect URI), 'NativeApp' for desktop/mobile apps, 'apiKey' for API key access (needs domain), 'iOS'/'Android' for mobile apps (needs urlScheme). Allowed values: `WebApp`, `SinglePageApp`, `NativeApp`, `apiKey`, `Web`, `iOS`, `Android`. |
| `defaultRedirectUri` | No | String | Required for WebApp, Web, and SinglePageApp platforms. Provide a plain URL (e.g. 'https://example.com/callback') — do not escape dots. |
| `urlScheme` | No | String | Required for iOS and Android platforms. The app URL scheme (e.g. 'myapp://callback'). |
| `redirectUriList` | No | Array of strings | Required for WebApp, Web, and SinglePageApp platforms. List of allowed redirect URI patterns. Pass plain URLs — the server escapes dots automatically. |
| `domain` | No | String | Required for apiKey platform — restricts which domains can use the key (e.g. 'www.example.com'). |
| `templateId` | No | String | Optional template ID. |
| `services` | No | Array of objects | Optional list of adobeid services to subscribe immediately. Item fields: `sdkCode` (String; required): The SDK code of the service to subscribe (e.g. 'CCEmbedCompanionAPI').; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Create a user OAuth credential for [platform] in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create Analytics Credential (`create_analytics_credential`)

Create an Analytics credential for a workspace. Supports Web, Android, and iOS platforms. Additional constraint: For `Web`, provide `defaultRedirectUri` and a non-empty `redirectUriList`. The platform description specifies `urlScheme` for mobile platforms.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `name` | Yes | String | Name for the credential. |
| `description` | Yes | String | Description for the credential. |
| `platform` | Yes | String (enum) | Platform type: 'Web' for web apps (requires defaultRedirectUri), 'iOS' and 'Android' for mobile apps (requires urlScheme instead). Allowed values: `Web`, `Android`, `iOS`. |
| `defaultRedirectUri` | No | String | Required for Web platform. Provide a plain URL (e.g. 'https://example.com/callback') — do not escape dots. |
| `urlScheme` | No | String | Required for iOS and Android platforms. The app URL scheme (e.g. 'myapp://callback'). |
| `redirectUriList` | No | Array of strings | Required for Web platform. List of allowed redirect URI patterns. Pass plain URLs — the server escapes dots automatically. |
| `domain` | No | String | Domain restriction for the credential. |

**Example prompt:**

* "Create an Analytics credential for [platform] in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create Admin Enterprise Credential (`create_admin_enterprise_credential`)

Create an Admin Enterprise (admin_entp) credential in a specific workspace.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `name` | Yes | String | Name for the admin enterprise credential. |
| `description` | Yes | String | Description for the admin enterprise credential. |
| `redirectUriPattern` | Yes | String | Regex pattern for allowed redirect URIs (e.g. 'https://.*\.example\.com/.*'). |
| `defaultRedirectUri` | Yes | String | The default redirect URI for OAuth callbacks. |
| `services` | No | Array of objects | Optional list of services to subscribe this credential to immediately. Item fields: `sdkCode` (String; required): The SDK code of the service to subscribe (e.g. 'AdobeAnalyticsSDK').; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Create an Admin Enterprise credential in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Update Admin Enterprise Credential (`update_admin_enterprise_credential`)

Update an existing Admin Enterprise credential's name, description, and redirect settings. This does not change API subscriptions. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `credentialId` | Yes | String | The admin enterprise credential ID (the 'id' field from get_credentials). |
| `name` | Yes | String | Name for the credential. |
| `description` | Yes | String | Description for the credential. |
| `redirectUriPattern` | Yes | String | Regex pattern for allowed redirect URIs (e.g. 'https://.*\.example\.com/.*'). |
| `defaultRedirectUri` | Yes | String | The default redirect URI for OAuth callbacks. |
| `services` | No | Array of objects | Legacy input retained for compatibility. The update endpoint does not change API subscriptions; omit this field. Item fields: `sdkCode` (String; required): The SDK code of the service to subscribe (e.g. 'AdobeAnalyticsSDK').; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Update Admin Enterprise credential [credentialId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Subscribe Credential To Services (`subscribe_credential_to_services`)

Subscribe a credential to one or more Adobe services. Works for all credential types (adobeid, analytics, entp, oauth_server_to_server). Each service needs at minimum an sdkCode. Already-subscribed services are automatically preserved — only pass the services you want to add or change. Preservation is per-service, not per-licenseConfig: passing a service with an sdkCode that's already subscribed replaces that service's entire licenseConfigs list, so include all of its intended licenseConfigs (existing plus new), not just the new one. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `credentialType` | Yes | String (enum) | Type of credential to subscribe services to. Allowed values: `adobeid`, `analytics`, `entp`, `oauth_server_to_server`. |
| `credentialId` | Yes | String | The credential ID (the 'id' field from get_credentials). |
| `services` | Yes | Array of objects | List of services to add or update. Each item needs at minimum an sdkCode. Already-subscribed services not listed here are kept as-is — you don't need to re-pass the full existing list. Item fields: `sdkCode` (String; required): The SDK code of the service to subscribe (e.g. 'AdobeAnalyticsSDK').; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Subscribe credential [credentialId] to the specified Adobe services."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Unsubscribe Credential From Service (`unsubscribe_credential_from_service`)

Remove one or more Adobe services from a credential's subscriptions. All other subscribed services are preserved. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `credentialType` | Yes | String (enum) | Type of the credential. Allowed values: `adobeid`, `analytics`, `entp`, `oauth_server_to_server`. |
| `credentialId` | Yes | String | The credential ID (the 'id' field from get_credentials). |
| `sdkCodes` | Yes | Array of strings | One or more SDK codes to remove (e.g. ['AdobeAnalyticsSDK']). All other existing subscriptions are preserved. Items: at least 1. |

**Example prompt:**

* "Remove service [sdkCode] from credential [credentialId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Subscribe Admin Enterprise Credential To Services (`subscribe_admin_enterprise_credential_to_services`)

Add or update API subscriptions for an Admin Enterprise credential. Existing services not included in the request are preserved. For an existing API, include all intended license configs and roles. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). Length: at least 1 characters. |
| `credentialId` | Yes | String | The Admin Enterprise credential ID (id_integration from get_credentials). Length: at least 1 characters. |
| `services` | Yes | Array of objects | Services to add or update. Existing services not listed here are preserved. For an existing SDK code, include all intended license configs and roles. Items: at least 1. Item fields: `sdkCode` (String; required) Length: at least 1 characters.; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Add or update API subscriptions for Admin Enterprise credential [credentialId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Unsubscribe Admin Enterprise Credential From Service (`unsubscribe_admin_enterprise_credential_from_service`)

Remove one API subscription from an Admin Enterprise credential. All other API subscriptions are preserved. Requires user approval. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations). Length: at least 1 characters. |
| `credentialId` | Yes | String | The Admin Enterprise credential ID (id_integration from get_credentials). Length: at least 1 characters. |
| `service` | Yes | Object | The single subscribed service to remove. Use its SDK code and any required subscription settings from the credential's current services. Fields: `sdkCode` (String; required) Length: at least 1 characters.; `atlasPlanCode` (String; optional); `licenseConfigs` (Array of objects; optional): License configs from list_services response. Item fields: `productId` (String; required); `id` (String; required); `op` (String; required).; `roles` (Array of objects; optional) Item fields: `id` (Number; required); `code` (String; required); `name` (String; required).. |

**Example prompt:**

* "Remove service [sdkCode] from Admin Enterprise credential [credentialId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Delete Credential (`delete_credential`)

Delete a credential from a workspace. Fails if the credential is still subscribed to any services — unsubscribe it from all services first. This is permanent and cannot be undone.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `orgId` | Yes | String | The numeric organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `projectId` | Yes | String | The project ID (the 'id' field from get_projects). |
| `workspaceId` | Yes | String | The workspace ID (the 'id' field from list_workspaces). |
| `credentialId` | Yes | String | The credential ID to delete (the 'id' field from get_credentials). |

**Example prompt:**

* "Delete credential [credentialId] from workspace [workspaceId]."

## Adobe I/O Events

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Event Providers (`list_event_providers`)

List all Adobe I/O event providers available to an organisation. Optionally filter by provider metadata ID or instance ID, and include event metadata for each provider. Additional constraint: Do not provide `providerMetadataId` and `providerMetadataIds` together.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | The consumer organisation ID (the 'id' field from get_organisations, e.g. '12345'). |
| `imsOrgCode` | Yes | String | The IMS org code (the 'code' field from get_organisations, e.g. 'ABC123@AdobeOrg'). |
| `providerMetadataId` | No | String | Filter by a single provider metadata ID. |
| `instanceId` | No | String | Filter by instance ID for multi-instance providers. |
| `providerMetadataIds` | No | Array of strings | Filter by multiple provider metadata IDs. Cannot be used together with providerMetadataId. |
| `eventmetadata` | No | Boolean | Whether to include event metadata for each provider. Defaults to false. |

**Example prompt:**

* "List event providers for my organization."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Provider Metadata (`get_provider_metadata`)

List all Adobe I/O event provider categories available to the org. Returns provider metadata entries grouped by category — use the 'id' field to filter list_event_providers. Requires the IMS org code (the 'code' field from get_organisations, e.g. 'ABC123@AdobeOrg').

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `imsOrgCode` | Yes | String | The IMS org code — use the 'code' field from get_organisations response (e.g. 'C74F69D7594880280A495D09@AdobeOrg'). |

**Example prompt:**

* "Show provider metadata for organization [imsOrgCode]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### List Provider Events (`list_provider_events`)

List the event metadata (event types) associated with a given provider. Use the provider ID returned by list_event_providers.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | The consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | The IMS org code (from get_organisations 'code' field, e.g. ABC123@AdobeOrg). |
| `providerId` | Yes | String | The provider ID — use the 'id' field from list_event_providers response. |

**Example prompt:**

* "List available event types for provider [providerId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create Event Registration (`create_event_registration`)

Create an event registration for a workspace. Subscribes to one or more event types from a provider and configures delivery via webhook, journal, or AWS EventBridge. Use list_event_providers to get provider IDs and list_provider_events to get event codes.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field, e.g. ABC123@AdobeOrg). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `client_id` | Yes | String | Client ID from Developer Console credential. Length: at least 3 and at most 128 characters. |
| `name` | Yes | String | Display name for the event registration. Length: at least 3 and at most 255 characters. |
| `description` | No | String | Optional description of the registration. Length: at most 5000 characters. |
| `webhook_url` | No | String | Webhook URL to deliver events to. Required for webhook/webhook_batch delivery types. Format: uri. Length: at most 4000 characters. |
| `events_of_interest` | Yes | Array of objects | Events to subscribe to. Use provider_id and event_code from list_event_providers / list_provider_events. Items: at least 1. Item fields: `provider_id` (String; optional): Provider ID from list_event_providers. Length: at least 1 and at most 38 characters.; `provider` (String; optional); `event_code` (String; required): Event code from list_provider_events. Length: at least 1 and at most 255 characters.. |
| `delivery_type` | Yes | String (enum) | How events are delivered. Allowed values: `webhook`, `webhook_batch`, `journal`, `aws_eventbridge`. |
| `runtime_action` | No | String | Optional Runtime action to invoke on events. Length: at most 255 characters. |
| `enabled` | No | Boolean | Whether the registration is enabled. Defaults to true. |
| `destination_metadata` | No | Object | Required for aws_eventbridge delivery type. Fields: `aws_region` (String; optional): AWS region for EventBridge delivery.; `aws_account_id` (String; optional): AWS account ID for EventBridge delivery.. |

**Example prompt:**

* "Create an event registration for workspace [workspaceId] and subscribe to [eventCode]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Registrations For Workspace (`get_registrations_for_workspace`)

Get all event registrations for a workspace. Shows all active registrations including delivery type, status, and subscribed events.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |

**Example prompt:**

* "List event registrations in workspace [workspaceId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Event Registration (`get_event_registration`)

Get details of a specific event registration by its registration ID. Returns full registration details including status, events, delivery type and webhook status.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID. |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `projectId` | Yes | String | Project ID. |
| `workspaceId` | Yes | String | Workspace ID. |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |

**Example prompt:**

* "Show details for event registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Update Event Registration (`update_event_registration`)

Update an existing event registration. Use this to change the name, events, delivery type, webhook URL, or enable/disable the registration. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID to update (from get_registrations_for_workspace). |
| `name` | Yes | String | Updated name for the registration. Length: at least 3 and at most 255 characters. |
| `description` | No | String | Length: at most 5000 characters. |
| `webhook_url` | No | String | Format: uri. Length: at most 4000 characters. |
| `events_of_interest` | Yes | Array of objects | Items: at least 1. Item fields: `provider_id` (String; optional); `provider` (String; optional); `event_code` (String; required) Length: at least 1 and at most 255 characters.. |
| `delivery_type` | Yes | String (enum) | Allowed values: `webhook`, `webhook_batch`, `journal`, `aws_eventbridge`. |
| `runtime_action` | No | String | Length: at most 255 characters. |
| `enabled` | No | Boolean | Whether the registration is enabled. |
| `destination_metadata` | No | Object | Fields: `aws_region` (String; optional); `aws_account_id` (String; optional). |

**Example prompt:**

* "Update the name or subscribed events for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Patch Event Registration (`patch_event_registration`)

Partially update a specific field of an event registration using JSON Patch (RFC 6902). Use this for targeted changes like enabling/disabling a registration or updating the name — without resending the full body. Use update_event_registration instead when you need to change multiple fields at once. Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID. |
| `projectId` | Yes | String | Project ID. |
| `workspaceId` | Yes | String | Workspace ID. |
| `registrationId` | Yes | String | Registration ID to patch. |
| `operations` | Yes | Array of objects | JSON Patch operations (RFC 6902). Examples: [&#123;op:'replace',path:'/enabled',value:false&#125;] Items: at least 1. Item fields: `op` (String (enum); required): JSON Patch operation. Allowed values: `add`, `remove`, `replace`, `move`, `copy`, `test`.; `path` (String; required): JSON pointer path e.g. '/enabled', '/name', '/webhook_url'.; `value` (Value; optional): New value (required for add/replace operations).. |

**Example prompt:**

* "Set registration [registrationId] to disabled."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Delete Event Registration (`delete_event_registration`)

Delete an event registration permanently. This is permanent and cannot be undone.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID. |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `projectId` | Yes | String | Project ID. |
| `workspaceId` | Yes | String | Workspace ID. |
| `registrationId` | Yes | String | Registration ID to delete (from get_registrations_for_workspace). |

**Example prompt:**

* "Delete event registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Tracing For Registration (`get_tracing_for_registration`)

Get event delivery trace details for a specific registration. Shows when events were delivered, their status, and trace metadata. Useful for debugging event delivery issues.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `credentialId` | Yes | String | Credential ID — use the 'id_integration' field from get_credentials response. |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |

**Example prompt:**

* "Show delivery traces for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Sample Event (`get_sample_event`)

Get a sample event payload for a given provider and event code. Returns the format and a sample JSON payload as it would appear in a webhook or journal delivery. Use check_sample_event first to confirm availability.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `providerId` | Yes | String | The provider ID from list_event_providers. |
| `eventCode` | Yes | String | The event code from list_provider_events. |

**Example prompt:**

* "Show a sample payload for event [eventCode]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Check Sample Event (`check_sample_event`)

Check if a sample event payload is available for a given provider and event code. Returns &#123; available: true &#125; if a sample exists, &#123; available: false &#125; if not.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `providerId` | Yes | String | The provider ID from list_event_providers. |
| `eventCode` | Yes | String | The event code from list_provider_events. |

**Example prompt:**

* "Check whether event [eventCode] has a supported sample payload."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Post Sample Event (`post_sample_event`)

Post a sample event to a specific registration for testing and debugging. Returns &#123; posted: true &#125; if the event was posted, &#123; posted: false &#125; if no sample payload is supported for this event type. Use get_sample_event to preview the payload first.

**Operation:** Sends a sample event to the selected registration.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `providerId` | Yes | String | The provider ID from list_event_providers. |
| `eventCode` | Yes | String | The event code from list_provider_events. |
| `registrationId` | Yes | String | The registration ID from create_event_registration. |
| `payload` | No | Object | Optional custom JSON event payload. Leave empty to use the default sample payload. Additional properties accept arbitrary values. |

**Example prompt:**

* "Send a sample event [eventCode] to registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Subscriber Filter Patterns (`get_subscriber_filter_patterns`)

List all supported Subscriber Defined Filter patterns with real examples in AWS Event Ruler JSON syntax. Use this to show users what filter patterns are available before they create a filter.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

This tool does not require any parameters.

**Example prompt:**

* "Show the supported Subscriber Defined Filter patterns with examples."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Subscriber Filters (`get_subscriber_filters`)

Retrieve all Subscriber Defined Filters for a given event registration. Returns a list of filters with their id, name, description, and filter expression (event-ruler syntax).

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |

**Example prompt:**

* "List filters for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Subscriber Filter (`get_subscriber_filter`)

Retrieve a specific Subscriber Defined Filter by its ID for a given event registration.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `subscriberFilterId` | Yes | String | The UUID of the Subscriber Defined Filter (from get_subscriber_filters 'id' field). Format: valid UUID. |

**Example prompt:**

* "Show filter [subscriberFilterId] for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Create Subscriber Filter (`create_subscriber_filter`)

Create a Subscriber Defined Filter for a given event registration. The filter expression uses event-ruler JSON syntax to match events. Returns the created filter with its assigned ID.

**Operation:** Creates a resource or submits a change.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `name` | Yes | String | Name of the Subscriber Defined Filter (3–80 characters). Length: at least 3 and at most 80 characters. |
| `description` | No | String | Optional description (up to 250 characters). Length: at most 250 characters. |
| `subscriber_filter` | Yes | String | Filter expression in event-ruler JSON syntax used to match events. |

**Example prompt:**

* "Create a filter for registration [registrationId] using the provided event-ruler expression."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Update Subscriber Filter (`update_subscriber_filter`)

Update an existing Subscriber Defined Filter for a given event registration. Replaces the name, description, and filter expression entirely (full update). Changes are saved with no automatic undo; review them before approving.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `subscriberFilterId` | Yes | String | The UUID of the Subscriber Defined Filter to update (from get_subscriber_filters 'id' field). Format: valid UUID. |
| `name` | Yes | String | Updated name of the Subscriber Defined Filter (3–80 characters). Length: at least 3 and at most 80 characters. |
| `description` | No | String | Updated description (up to 250 characters). Length: at most 250 characters. |
| `subscriber_filter` | Yes | String | Updated filter expression in event-ruler JSON syntax. |

**Example prompt:**

* "Update filter [subscriberFilterId] for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Delete Subscriber Filter (`delete_subscriber_filter`)

Delete a specific Subscriber Defined Filter permanently. This is permanent and cannot be undone.

**Operation:** Modifies or removes an existing resource; the client requests user approval.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `subscriberFilterId` | Yes | String | The UUID of the Subscriber Defined Filter to delete (from get_subscriber_filters 'id' field). Format: valid UUID. |

**Example prompt:**

* "Delete filter [subscriberFilterId] from registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Validate Subscriber Filter (`validate_subscriber_filter`)

Validate a Subscriber Defined Filter expression against the registration's existing event codes. Optionally provide custom sample events to test the filter against. Returns the validation result showing which events would match.

**Operation:** Submits a filter validation request; it does not save the filter.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `projectId` | Yes | String | Project ID (from get_projects). |
| `workspaceId` | Yes | String | Workspace ID (from list_workspaces). |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `subscriber_filter` | Yes | Object | The Subscriber Defined Filter to validate. Fields: `id` (String; optional): Optional filter ID if validating an existing filter. Format: valid UUID.; `name` (String; required): Name of the filter (3–80 characters). Length: at least 3 and at most 80 characters.; `description` (String; optional): Optional description (up to 250 characters). Length: at most 250 characters.; `subscriber_filter` (String; required): Filter expression in event-ruler JSON syntax to validate.. |
| `custom_sample_events` | No | Array of objects | Optional custom sample events to test the filter against. Each object is a CloudEvent payload. Safe to omit if you only want to validate the filter's syntax — a non-empty array currently returns a 400 from the upstream API regardless of content, so avoid passing real sample events until that's resolved upstream. |

**Example prompt:**

* "Validate this event filter for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Get Journal Events Batch (`get_journal_events_batch`)

Fetch a batch of events from the journal for a registration. Unlike get_journal_events, all positioning params are optional: omit all to read from the beginning, use `since` (cursor from `_page.last`) to paginate, use `seek` (ISO 8601 duration, e.g. '-PT2H') to jump to a point in time, or set `latest: true` to start from the most recent events. `since` and `seek` cannot be combined. Additional constraint: Do not combine `since` and `seek`.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `credentialId` | Yes | String | Credential ID — use the 'id_integration' field from get_credentials response. |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `since` | No | String | Journal cursor to fetch events after. Use '_page.last' from a previous response. Cannot be combined with 'seek'. |
| `seek` | No | String | ISO 8601 duration to seek to a point in time (e.g. '-PT2H' for 2 hours ago, '-P1D' for 1 day ago). Cannot be combined with 'since'. |
| `latest` | No | Boolean | Jump to the end of the journal to start consuming the most recent events. |
| `limit` | No | Integer | Maximum number of events to return (1–100). Fewer may be returned if total payload exceeds 1.5 MB. Range: at least 1 and at most 100. |
| `urlLinks` | No | Boolean | Include URL links in the response payload. |

**Example prompt:**

* "Fetch the latest journal events for registration [registrationId]."

<AccordionItem slots="heading, text, text, text, table, text, text"/>

### Validate And Get Journal Events (`validate_and_get_journal_events`)

Validate a cursor position and fetch events from the journal starting from that position. The `since` parameter is required — it must be a cursor from a previous response's `_page.last` field (format: 'camel:…'). Use `get_journal_events_batch` first to get an initial cursor, then use this tool to paginate from a known position.

**Operation:** Read-only; does not change Adobe resources.

**Parameters:**

| Name | Required | Type | Description |
|------|----------|------|-------------|
| `consumerOrgId` | Yes | String | Consumer organisation ID (from get_organisations 'id' field). |
| `imsOrgCode` | Yes | String | IMS org code (from get_organisations 'code' field). |
| `credentialId` | Yes | String | Credential ID — use the 'id_integration' field from get_credentials response. |
| `registrationId` | Yes | String | Registration ID (from get_registrations_for_workspace). |
| `since` | Yes | String | Journal cursor position to fetch events from. Use the '_page.last' value from a previous get_journal_events response to paginate. Format: 'camel:&#123;uuid&#125;.camel:&#123;uuid&#125;.&#123;event-id&#125;…'. Required — the endpoint does not accept 'HEAD' or an empty value. |
| `limit` | No | Integer | Maximum number of events to return (1–100). Fewer may be returned if total payload exceeds 1.5 MB. Range: at least 1 and at most 100. |
| `urlLinks` | No | Boolean | Include URL links in the response payload. Defaults to false. |

**Example prompt:**

* "Fetch journal events from cursor [since] for registration [registrationId]."
