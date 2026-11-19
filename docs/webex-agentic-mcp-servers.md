---
type: Guide
title: Agentic Apps | Webex MCP Server Usage Guide
display_title: Overview
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers)

This guide helps developers integrate Webex MCP (Model Context Protocol) servers with popular AI clients. MCP enables AI agents to securely access Webex capabilities through the Model Context Protocol.

## Overview

Webex provides MCP servers that enable AI agents to securely access various Webex functionalities through the Model Context Protocol. These servers act as a bridge between your AI client and Webex services, allowing AI agents to perform actions and retrieve information on your behalf.

## Authentication

Webex MCP servers support two authorization methods: Token-Based authentication and OAuth 2.0. Please verify the required authentication approach before generating the token.

### 1. Token-Based Authentication

Use a WCIT (Webex Client Identity Token) to authenticate with Webex MCP servers. The WCIT is issued with only the `spark:mcp` scope which will allow to connect to MCP server. Additional scopes required by specific tools are requested at runtime via MCP elicitation during too call.

> **Note**: This method only works with clients that support MCP elicitation. If your client does not support elicitation, use OAuth 2.0 instead.
>
> **What is MCP elicitation?** Elicitation is a capability in the MCP protocol that allows an MCP server to request additional information from the user during a tool call — for example, prompting the user to grant consent for specific OAuth scopes. When using a WCIT token, the initial connection uses only the `spark:mcp` scope. When a tool requires additional scopes (e.g., `meeting:schedules_read`), the server uses elicitation to ask the user to authorize those scopes in real time. Clients that support elicitation can handle this flow seamlessly; clients that do not will fail on tools requiring additional scopes.

1. Navigate to the [Generate WCIT Token](https://developer.webex.com/agentic-token) page in the Webex Developer Portal
2. Enter an appropriate name for your token
3. Click **Generate New Token**
4. Copy the generated token and store it securely (you'll need this for configuration)

> **Important**: Keep your token secure and never commit it to version control.

### 2. OAuth 2.0

OAuth 2.0 can be used by clients that do not support elicitation. This requires creating a Webex Integration with the appropriate scopes.

1. Navigate to the [Create a New Integration](https://developer.webex.com/my-apps/new/integration) page
2. Fill in the form:
   - **Will this integration use a mobile SDK?** No
   - **Integration name:** Give any name
   - **Icon:** Choose one of the default icons
   - **App Hub Description:** Give any description
   - **Redirect URI(s):** You'll get this from the OAuth configuration page in your client
   - **Scopes:** Select the scopes required by your MCP server along with `spark:mcp`. To find the required scopes, go to the [Agentic Apps](https://apphub.webex.com/agentic-apps) page, choose your server, and click **Learn More** to open the MCP Server product page in Developer Portal where the required scopes are listed.
5. Click **Add Integration** to create your integration
6. On the following screen note down the **Client ID** and **Client Secret** — you won't be able to read your Client Secret again once you leave this page

## Configure Your AI Client

Choose your AI client below and follow the configuration guide:

- [Amazon Quick](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick)
- [Claude Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-code)
- [Claude Desktop](https://developer.webex.com/docs/webex-agentic-mcp-servers-claude-desktop)
- [Codex](https://developer.webex.com/docs/webex-agentic-mcp-servers-codex)
- [Copilot Studio](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio)
- [Cursor](https://developer.webex.com/docs/webex-agentic-mcp-servers-cursor)
- [Gemini CLI](https://developer.webex.com/docs/webex-agentic-mcp-servers-gemini-cli)
- [VS Code](https://developer.webex.com/docs/webex-agentic-mcp-servers-vscode)

---

## Troubleshooting

### Common Issues

#### Connection Failed

**Problem**: MCP server fails to connect

**Solutions**:
- Verify your WCIT token is valid and not expired
- Check that the endpoint URL is correct
- Ensure you have an active internet connection

#### Authentication Error

**Problem**: "401 Unauthorized" or authentication errors

**Solutions**:
- Regenerate your WCIT token from the Developer Portal
- Ensure the token is properly formatted with "Bearer " prefix in the configuration
- Check that the token hasn't been revoked

#### Server Not Responding

**Problem**: MCP server is not responding to requests

**Solutions**:
- Verify your firewall isn't blocking the connection
- Try restarting your AI client

#### Tools Not Appearing

**Problem**: Webex tools don't show up in the AI client

**Solutions**:
- Confirm the configuration file syntax is correct (valid JSON)
- Restart the AI client completely
- Check the AI client's console/logs for error messages
- Verify you're using the latest version of your AI client:
  - **Claude Desktop**: Check for updates via Claude menu > "Check for Updates..."
  - **VS Code**: Ensure GitHub Copilot extension is up to date
  - **Cursor**: Check for IDE updates in Cursor settings

### Getting Help

If you continue to experience issues, visit the [Webex Developer Support](https://developer.webex.com/explore/support).

## Managing Your MCP Connection

### Unlinking an MCP Server

If you need to remove an MCP server from your AI client:

**Claude Desktop:**
1. Open Settings > Developer tab
2. Click "Edit Config" to open `claude_desktop_config.json`
3. Remove the server entry from the `mcpServers` object
4. Save the file and restart Claude Desktop

**VS Code:**
1. Use Command Palette: **MCP: Remove Server** and select the server to remove, or
2. Manually edit `mcp.json` (global or workspace) and remove the server entry from the `servers` object
3. Reload the VS Code window

**Cursor IDE:**
1. Open Cursor Settings > Tools & Integrations > MCP Tools
2. Remove the server entry from `~/.cursor/mcp.json`
3. Save the file (Cursor will automatically detect the change)

### Revoking Your WCIT Token

If your token is compromised or you no longer need it:

1. Navigate to the **Manage WCIT Tokens** page in the Webex Developer Portal
2. Locate the token you want to revoke in the list
3. Click the **Delete** button next to the token
4. Confirm the revocation

> **Important**: After revoking a token, any AI clients using that token will immediately lose access to Webex MCP servers. You'll need to generate a new token and update your client configurations.

## Next Steps

Now that you've connected your Webex MCP server, you can:

- Explore the available Webex capabilities in your AI client
- Build custom workflows using Webex messaging and collaboration features
- Create intelligent agents that interact with your Webex organization

---

**Last Updated**: February 2, 2026

**Questions or Feedback?** Visit the [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers) or contact support through the Developer Portal.
