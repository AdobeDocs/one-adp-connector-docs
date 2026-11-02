---
title: Connect to ChatGPT
description: Connect to Adobe Analytics and Customer Journey Analytics MCP servers using ChatGPT.
---
# Connect to ChatGPT

You can request Adobe Analytics and Customer Journey Analytics data using ChatGPT.

<InlineAlert variant="warning" slots="text"/>

You must be on the "Plus" or "Pro" subscription to ChatGPT. OpenAI does not allow connecting to MCP servers using their "Free" tier.

The connection steps differ by product. Use [Customer Journey Analytics](#customer-journey-analytics) to add the CJA plugin, or [Adobe Analytics](#adobe-analytics) to add the Adobe Analytics MCP server manually.

## Customer Journey Analytics

Adobe publishes Customer Journey Analytics as a plugin in ChatGPT, so you can add it directly without enabling Developer mode or entering a server URL.

1. Verify that your account has MCP access for Customer Journey Analytics. See [Set up permissions](permissions.md).
1. Log in to [ChatGPT](https://chatgpt.com) using your credentials.
1. Open the **Plugins** section.
1. In the search box, type `CJA`.
1. Select **Install plugin**.
1. When prompted, authenticate using your Adobe ID credentials. Ensure that you select the desired IMS org if your Adobe ID belongs to more than one.

The Customer Journey Analytics plugin home lists several options for analyzing data in your organization. You can also open chat within the context of the plugin by selecting "Try in chat." Once installed, you can invoke the plugin by mentioning it with `@Customer Journey Analytics` in any prompt, as shown below:

```text
"@Customer Journey Analytics Show me visits and revenue by marketing channel for the last 30 days in my main data view"
```

## Adobe Analytics

Add the Adobe Analytics MCP server manually using Developer mode.

1. Verify that your account has MCP access for Adobe Analytics. See [Set up permissions](permissions.md).
1. Log in to [ChatGPT](https://chatgpt.com) using your credentials.
1. In the lower left, select **your name** &rarr; **Settings**.
1. Select **Apps**, then enable **Developer mode**.
1. Select the **Create app** button.
1. Give the app a desired name (such as "Adobe Analytics") and enter the MCP Server URL: `https://aa-mcp.adobe.io/mcp`
1. Ensure that Authentication is set to **OAuth** (set by default), and select the acceptance check box to continue.
1. Once the app is created, a login window pops up. Authenticate using your Adobe ID credentials. Ensure that you select the desired IMS org if your Adobe ID belongs to more than one.

The tool is ready for use. You can converse with ChatGPT in the context of your Analytics environment by invoking the tool:

```text
"Use the Adobe Analytics tool to show me what report suites are available."
```
