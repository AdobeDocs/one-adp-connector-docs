---
title: Install the plugin in Claude
description: Install the Adobe for Developers plugin and its skills in Claude Code or Claude Desktop.
---

# Install in Claude

The Adobe for Developers plugin includes tools together with companion skills — guided flows for common Adobe Developer Platform tasks. You need both for the full experience.

## Claude Code

This is the fastest path — one install gives you both the tools and the skills.

1. Open Claude Code.
1. Add the marketplace:

   ```shell
   /plugin marketplace add adobe/skills
   ```

1. Install the plugin:

   ```shell
   /plugin install adobe-for-developers-connector@adobe-skills
   ```

1. Confirm the install: type `/` in the chat and check that the Adobe for Developers skills appear in the list.

That's it. The plugin's tools and all skills are now active.

## Claude Desktop

On Claude Desktop, install the plugin to add its companion skills. Connecting the plugin's MCP server is a separate step. Whether you can connect it directly from Claude's **Connectors** tab depends on your plan and organization settings.

### 1. Install the skills through the plugin

1. Open Claude Desktop.
1. Go to **Settings > Plugins > Add marketplace**.
1. Add the marketplace: `adobe/skills`. Claude Desktop will warn that marketplace plugins are not verified by Anthropic — this is expected; proceed.
1. Install the `adobe-for-developers-connector` plugin from the marketplace.
1. Check the plugin's skills list. All skills should now be available in chat.

After installing the plugin, check its **Connectors** tab. If the **Install** button is available, use it to connect the server and follow the sign-in prompts. If direct installation is unavailable, and your organization's policies allow custom MCP server connections, use the manual setup below. If organization settings prevent you from adding MCP server connections, contact your Claude organization owner or administrator.

### Manual MCP server setup

Use this option only if direct installation is unavailable and your organization's policies allow manually configured MCP server connections.

1. Locate your Claude Desktop config file:

   * **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   * **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

1. Add the plugin's MCP server under `mcpServers`, using the `mcp-remote` bridge:

   ```json
   {
     "mcpServers": {
       "adobe-for-developers-connector": {
         "command": "npx",
         "args": ["mcp-remote@latest", "https://adp-connector.adobe.io/mcp"]
       }
     }
   }
   ```

   If the file already has other entries under `mcpServers`, add `adobe-for-developers-connector` alongside them rather than replacing the file.

1. Save the file.
1. Fully quit Claude Desktop (Cmd+Q on macOS) and reopen it. A restart, not just closing the window, is required for the config to load.
1. Confirm the plugin's tools are available: start a new chat and check that Claude can call Adobe for Developers tools — for example, ask it to list your Developer Console projects.
