---
type: Guide
title: Webex MCP Server Usage Guide | Copilot Studio
display_title: Copilot Studio
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-copilot-studio)

---

This guide walks you through how you can connect your agent in Copilot Studio to Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Use the MCP Onboarding Wizard

The simplest way to connect to an existing MCP server is directly within Copilot Studio using the MCP onboarding wizard.

There are two parts to this method:

- Configure the basic MCP server details
- Configure authentication with your MCP server

## Configure Basic Server Details

1. Go to the **Tools** page for your agent
2. Select **Add a tool**
3. Select **New tool**
4. Select **Model Context Protocol**. The MCP onboarding wizard appears.
5. Fill in the required fields: **Server name**, **Server description**, and **Server URL**
6. Select the authentication type for the MCP server as **OAuth 2.0**
7. Select **Manual** as the OAuth 2.0 type. More fields will appear for you to configure the OAuth 2.0 settings.

> Make sure to write a brief, but clear description of what your MCP server does. The agent orchestrator uses this information to identify whether to call your server at runtime.

## OAuth Configuration

Fill in the required fields — **Client ID** and **Client secret** are from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20):

- **Client ID**
- **Client secret**
- **Authorization URL:** `https://webexapis.com/v1/authorize`
- **Token URL template:** `https://webexapis.com/v1/access_token`
- **Refresh URL:** `https://webexapis.com/v1/access_token`
- **Scopes:** The permissions your app is asking for, as a space-separated list

Select **Create** to add the server. A callback URL appears.

Copy the callback URL to add to your application's registration when creating your Webex OAuth 2.0 Integration.

Select **Next** to continue.

## Create a New Connection and Add the MCP Server to Your Agent

1. On the **Add tool** dialog, select **Create a new connection** for your MCP server or use an existing one
2. Select **Add to agent** to finish adding the MCP server to your agent

## Resources

- [Copilot Studio Official Documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/agent-extend-action-mcp)
