---
title: Adobe for Developers plugin skills
description: An overview of the task-focused skills included with the Adobe for Developers plugin.
---

# Adobe for Developers plugin skills

Skills are task-focused playbooks included with the Adobe for Developers plugin. They help your agent choose and sequence plugin tools to complete common workflows. They use the organizations, projects, workspaces, and permissions available to your signed-in account; you can select the organization to use when prompted.

## Developer Console

### Developer Console context (`dev-console-context`)

Helps you find organizations, projects, workspaces, and credentials available to your signed-in account. You can inspect project details, choose the resources for a task, and keep track of your selected context.

### Create a Developer Console project (`dev-console-create-project`)

Creates and initializes a Developer Console project in your selected organization. It can set up a default project or an App Builder template project, resolve an available name, and prepare the required workspaces.

### Subscribe to an Adobe API (`dev-console-subscribe-api`)

Guides you through adding an Adobe API to a project: find the available API, choose a workspace and supported credential type, select any required product profiles, and create a credential if needed.

### Remove an API subscription (`dev-console-unsubscribe-api`)

Removes one or more API subscriptions from a credential in the selected workspace. Shows the current subscriptions and preserves any APIs you have not chosen to remove.

## Documentation search

### Search Adobe developer documentation (`search-adobe-developer-docs`)

Searches official Adobe developer documentation and returns relevant passages with source links for your AI agent to synthesize into an answer. It is used for questions about Adobe products, APIs, SDKs, and platform concepts, and to ground setup and provisioning guidance in current documentation.

## IO Events

### Manage I/O Events registrations (`io-events-registration`)

Guides you through creating and managing event registrations. It helps select an organization, project, workspace, event provider, event types, credential, and delivery method, and supports journal reading, delivery tracing, webhook verification, updates, and deletion.

### Filter and test I/O Events (`io-events-filtering`)

Helps inspect sample event payloads, send sample events for testing, and create, validate, update, or delete Subscriber Defined Filters. It uses the event registration context when working with a specific registration.

## App Builder

### Set up App Builder development (`app-builder-setup`)

Checks that Node.js, the Adobe I/O CLI, and your Adobe sign-in are ready for App Builder development. Helps resolve tooling issues and confirm your organization, access, and Developer Terms, making changes only with your approval.

### Create an App Builder app (`app-builder-create-app`)

Creates an App Builder app or UI extension from your requirements, including project setup, a suitable template, and the required UI and actions. Starts a local preview so you can try the app before deploying.

### Deploy an App Builder app (`app-builder-deploy`)

Deploys your App Builder app to Stage or Production. Checks the app and target workspace, compares API subscriptions before Production deployment, and confirms the changes with you. Reports whether deployment completed or was skipped.

### Troubleshoot an App Builder app (`app-builder-troubleshoot`)

Investigates App Builder app and action failures using recent runs and redacted logs. Groups repeated errors, explains likely causes, and suggests fixes; changes are made only after your approval.
