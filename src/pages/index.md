---
title: Adobe for Developers plugin
description: Search, build, and distribute right from your AI coding agent.
---

<Superhero slots="image, heading, text, buttons" background="rgb(37, 37, 37)"/>

![Adobe for Developers banner](assets/adobe-for-developers-hero-wide-banner.svg)

# Adobe for Developers plugin

Search, build, and distribute right from your AI coding agent.

[Get started](guides/index.md)

<Resources slots="heading, links"/>

#### Resources

* [Getting started](guides/index.md)
* [Tools](guides/reference.md)
* [Skills](guides/skills.md)
* [Github repository](https://github.com/AdobeDocs/one-adp-connector-docs)

## Overview

The Adobe for Developers plugin helps you complete common Adobe developer workflows directly from your AI coding agents.

Use the plugin to:

* Search [Adobe's developer documentation](https://developer.adobe.com/) and get clear answers with links to the source pages
* Set up an Adobe API, including its [Developer Console](https://developer.adobe.com/console/) project and credentials
* Add more APIs to an existing project or credential
* Subscribe to Adobe I/O Events through webhooks or a journal, with optional filters
* Send sample events to test your setup and find out why events are not arriving
* Open the Developer Console to view a credential's client secrets
* Review the projects, workspaces, and credentials you already have

See [Getting started](guides/index.md) to connect the plugin to your client. See the [tool reference](guides/reference.md) and [skills](guides/skills.md) for a complete list of available tools and their parameters.

<InlineAlert variant="warning" slots="text, text"/>

The Model Context Protocol (MCP) is an open-source standard that can introduce security and reliability risks. Connecting MCP clients or servers to Adobe products is a customer-elected configuration. Customers are responsible for evaluating the security and suitability of any MCP integration. Adobe is not responsible for issues arising from misconfiguration, misuse, third-party vulnerabilities, or unintended actions performed through MCP-enabled workflows.

To reduce risk, test integrations in a sandbox environment before production use. Validate all MCP-initiated actions and responses before acting on them.
