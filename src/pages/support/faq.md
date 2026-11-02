---
title: Adobe for Developers Connector FAQ
description: Answers to common questions about the Adobe for Developers plugin and its skills.
---

# Frequently asked questions

Common questions about using the Adobe for Developers plugin.

## Getting started

<AccordionItem slots="heading, text"/>

### What is the Adobe for Developers Plugin?

The Adobe for Developers plugin combines tools and task-focused skills for working with Adobe developer products. It can search official Adobe developer documentation, manage Developer Console projects, workspaces, credentials and API subscriptions, and configure Adobe I/O Events. See the [tool reference](../guides/reference.md) and [skills overview](../guides/skills.md).

<AccordionItem slots="heading, text"/>

### Which clients are covered by the installation guide?

The current installation guide covers Claude Code and Claude Desktop. See the [Claude installation guide](../guides/quick-start/claude.md) for the steps and any client-specific setup.

<AccordionItem slots="heading, text"/>

### Can I use the plugin with an Adobe organization I belong to?

The Connector uses your signed-in Adobe identity. It can show organizations that identity can access, and you can select the organization relevant to your task. What you can view or change depends on your access and permissions in that organization; the plugin does not grant additional access.

<AccordionItem slots="heading, text"/>

### How do I sign in?

Connect through the supported Claude client and complete the Adobe sign-in prompt. The Connector acts on behalf of your authenticated Adobe account, rather than using a shared user account. If the wrong Adobe account is signed in, switch accounts in Claude and reconnect.

## Developer Console

<AccordionItem slots="heading, text"/>

### What can I do in Developer Console with the plugin?

Depending on your access, you can find projects and workspaces, create or update projects and credentials, inspect credential subscriptions, and subscribe or unsubscribe APIs. The [tool reference](../guides/reference.md) lists the available operations and their inputs.

<AccordionItem slots="heading, text"/>

### Why is the Adobe Developer Terms prompt shown?

Most Developer Console operations that manage organization resources require the Adobe Developer Terms to be accepted for the selected organization. Review the terms before agreeing. The Connector only accepts them after you explicitly confirm that you agree.

<AccordionItem slots="heading, text"/>

### Which credential types can the plugin work with?

The Connector includes tools for OAuth Server-to-Server, User Auth (AdobeId), Analytics, and Admin Enterprise credentials. Which types are supported for an API depends on the API and your organization's access. The API subscription skill checks the available options before proceeding.

<AccordionItem slots="heading, text"/>

### Why can’t I see or change a project, API, or credential?

The Connector only returns resources available to your signed-in Adobe account in the selected organization. Confirm the organization and project context, then check with your organization administrator if you need additional access or product permissions.

## Adobe I/O Events

<AccordionItem slots="heading, text"/>

### What can I do with Adobe I/O Events?

You can discover providers and event types, create and manage event registrations, and configure supported delivery methods such as webhooks, journals, or AWS EventBridge. You can also inspect delivery traces and read journal events. Available options depend on your organization and the selected project, workspace, and credential.

<AccordionItem slots="heading, text"/>

### Can I test an event or manage event filters?

Yes. The Connector can check for and display supported sample payloads, post a sample event to a registration, and create, validate, update, list, or delete Subscriber Defined Filters. Review the selected registration and payload before sending a test event.

## Approvals and privacy

<AccordionItem slots="heading, text"/>

### Why does Claude ask me to approve an action?

Some tools modify or remove projects, credentials, API subscriptions, registrations, or filters. Compatible clients display an approval prompt for actions marked as destructive or high impact. Review what the action will change before approving it; permanent deletions cannot be undone.

<AccordionItem slots="heading, text"/>

### Does the Connector generate answers with an AI model?

No. The Connector provides tools and retrieves documentation passages; Claude interprets your request and synthesizes the response. For documentation searches, the retrieved passages and source links are returned to Claude so it can answer your question.

<AccordionItem slots="heading, text"/>

### Is my data used to train AI models?

That depends on your Claude plan, settings, and agreement with Anthropic, not on this documentation. Review Anthropic's data-use terms for your account. Your organization may also have policies governing the use of AI clients with Adobe data.

<AccordionItem slots="heading, text"/>

### Where can I report an issue or ask for help?

For general Adobe developer product support, visit [Adobe Developer Support](https://developer.adobe.com/developer-support/). To report an issue with this documentation, use the [documentation repository issue tracker](https://github.com/AdobeDocs/one-adp-connector-docs/issues).
