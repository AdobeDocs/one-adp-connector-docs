---
title: Connect to Cursor
description: Connect to Adobe Analytics and Customer Journey Analytics MCP servers using Cursor.
---
# Connect to Cursor

You can request Adobe Analytics and Customer Journey Analytics data using Cursor.

1. Verify that your account has MCP access for the desired product. See [Set up permissions](permissions.md).
1. Launch the [Cursor IDE](https://cursor.com) and authenticate using your credentials.
1. Navigate to **File** &rarr; **Preferences** &rarr; **Cursor settings**.
1. Select the **Tools & MCPs** section.
1. Select **Add Custom MCP**. The file `mcp.json` is opened.
1. Add the desired product to the JSON entry. If you added both Adobe Analytics and Customer Journey Analytics simultaneously, your JSON file might look similar to the following:

    ```json
    {
      "mcpServers": {
        "Customer Journey Analytics": {
          "type": "streamable-http",
          "url": "https://cja-mcp.adobe.io/mcp"
        },
        "Adobe Analytics": {
          "type": "streamable-http",
          "url": "https://aa-mcp.adobe.io/mcp"
        }
      }
    }
    ```

1. Select **File** &rarr; **Save**. Close `mcp.json`.
1. Back in Tools & MCPs, the desired MCP tool(s) are visible.
1. Select **Connect** next to the desired MCP tool.
1. A login window pops up. Authenticate using your Adobe ID credentials. Ensure that you select the desired IMS org if your Adobe ID belongs to more than one.
1. Approve the connection between Adobe and Cursor.
1. Open a fresh chat window with Cursor.

The tool is ready for use. You can converse with Cursor in context of your Analytics environment by invoking the tool:

```text
"Use the Adobe Analytics tool to show me what report suites are available."
"Use the Customer Journey Analytics tool to show me what data views are available."
```
