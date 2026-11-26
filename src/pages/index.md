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

The **Adobe for Developers** plugin brings the capabilities of Adobe's developer platform into the AI coding agent you already use. Describe what you want to build, and your agent draws on [Adobe's documentation](https://developer.adobe.com/) and [Developer Console](https://developer.adobe.com/console) to find the right API, set up access, wire up events, start your app, and help you reach customers.

You don't need to know Adobe's terminology. Say "I want to call the Adobe Firefly API" or "notify my webhook when my Lightroom job finishes", and your agent guides you through the choices and does the setup. It works with the same projects, credentials, and events you see in the Developer Console.

### What you get

* **Answers grounded in Adobe's documentation.** Ask a question about Adobe's APIs, SDKs, and platform, and get a clear answer with links to the source pages.
* **Setup by conversation.** Your agent creates the [Developer Console](https://developer.adobe.com/console/) project, adds the API, and creates the credential. Add more APIs to an existing project or credential as your app grows. Review the projects, workspaces, and credentials you already have, or open the Developer Console to view a client secret.
* **Events, ready to receive.** Subscribe to Adobe I/O Events at your webhook or read them from a journal. You can also send sample events to test your setup, and find out why events are not arriving.
* **A running start on App Builder.** Create the project and workspaces, select a template, get starter code, and deploy, all from your agent. App Builder setup uses the Adobe I/O CLI on your computer, so you need Node.js and the CLI installed, and a desktop or command-line client such as Claude or GitHub Copilot.
* **A path to your customers.** Create and manage your Adobe Exchange listings and versions, and submit them for review, from the same conversation. Coming soon.

### Why connect it

* **Work where you already work.** Search, set up, build, and distribute from your AI coding agent, with Adobe's platform behind it.
* **Go from idea to a working API call quickly.** Whether you are new to Adobe or have built on it for years, your agent handles the setup so you can focus on your goal.
* **Your account, your access.** You sign in with your Adobe ID, and your agent can only see and change what your account already has access to.

### Get started

Connect the plugin to Claude or GitHub Copilot, sign in with your Adobe ID, and start asking. See [Getting started](guides/index.md) to connect the plugin to your client, and the [tool reference](guides/reference.md) and [skills](guides/skills.md) for the complete list.

<InlineAlert variant="warning" slots="text, text"/>

The Model Context Protocol (MCP) is an open-source standard that can introduce security and reliability risks. Connecting MCP clients or servers to Adobe products is a customer-elected configuration. Customers are responsible for evaluating the security and suitability of any MCP integration. Adobe is not responsible for issues arising from misconfiguration, misuse, third-party vulnerabilities, or unintended actions performed through MCP-enabled workflows.

To reduce risk, test integrations in a sandbox environment before production use. Validate all MCP-initiated actions and responses before acting on them.
