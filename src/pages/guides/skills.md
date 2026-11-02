---
title: Adobe for Developers plugin skills
description: An overview of the task-focused skills included with the Adobe for Developers plugin.
---

# Adobe for Developers plugin skills

Skills are task-focused playbooks included with the Adobe for Developers plugin. They help Claude choose and sequence connector tools to complete common workflows. They use the organizations, projects, workspaces, and permissions available to your signed-in account; you can select the organization to use when prompted.

## Available skills

### Developer Console context (`dev-console-context`)

Establishes and tracks your selected organization, project, workspace, and optionally credential. It displays the current context as a breadcrumb and is used at the start of API subscription and I/O Events workflows.

Use it when you want to explore your Developer Console projects, workspaces, or credentials, or when you need to choose the context for another workflow.

### Subscribe to an Adobe API (`dev-console-subscribe-api`)

Guides you through finding an API, selecting a project and workspace, choosing a credential type, reviewing any available product profiles, and subscribing the API. It can help create a project or credential when needed and also supports removing an API subscription.

Use it when you need access to an Adobe API or want to manage an API subscription.

### Search Adobe developer documentation (`search-adobe-developer-docs`)

Searches official Adobe developer documentation and returns relevant passages with source links for Claude to synthesize into an answer. It is used for questions about Adobe products, APIs, SDKs, and platform concepts, and to ground setup and provisioning guidance in current documentation.

### Manage I/O Events registrations (`io-events-registration`)

Guides you through creating and managing event registrations. It helps select an organization, project, workspace, event provider, event types, credential, and delivery method, and supports journal reading, delivery tracing, webhook verification, updates, and deletion.

### Filter and test I/O Events (`io-events-filtering`)

Helps inspect sample event payloads, send sample events for testing, and create, validate, update, or delete Subscriber Defined Filters. It uses the event registration context when working with a specific registration.
