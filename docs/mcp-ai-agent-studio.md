---
type: Guide
title: MCP | AI Agent Studio
display_title: AI Agent Studio
canonical_url: https://developer.webex.com/docs/mcp-ai-agent-studio
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/mcp-ai-agent-studio)

## Configure MCP Client Action

The Model Context Protocol (MCP) client capability enables autonomous AI agents to connect directly to third-party tools and services without requiring custom-built API integrations. This streamlines how agents retrieve data and perform actions during live customer conversations.

By setting up an MCP client, your AI agents can:

- Automatically invoke third-party tools during live conversations
- Retrieve real-time data from external systems
- Perform actions without human intervention

### Prerequisites

Before you configure an MCP action in the Webex AI Agent Studio, you must have:

- The MCP server URL
- Authentication type and credentials for the third-party service

> **Note:** MCP actions are read-only once created. If you need to change action settings, you must create a new action.

### Steps

**1.** Log in to the Webex AI Agent Studio platform.

**2.** Choose the AI agent for which you want to configure the MCP action. You can also create a new autonomous AI agent. See the *Create an autonomous AI agent* section for more information.

**3.** Navigate to the **Actions** tab. Click **+ Add actions**.

**4.** In the **Add actions** pop-up, under **Browse actions**, choose **Select available**.

This displays all the available MCP tools with the provider name and MCP label.

> **Note:** AI Agent Studio displays MCP tools that use a supported authentication method. MCP tools configured with OAuth 2.0 Authorization Code are not currently displayed in the available actions list.

**5.** Choose the MCP tool you want to add. You can add multiple MCP tools at any time. Click **Add**.

> Your agent can support a maximum number of actions as defined by your organization's configuration.

### What to Do Next

Once an MCP tool is added, the system automatically populates the following details from the MCP server definition:

- **Action name** — MCP tool name
- **Description**
- **Input entities** — Required fields and data types

If you need to modify any of these details, you must update the MCP server definition at the registration or provisioning stage. Changes get synchronized automatically to the AI Agent Studio via notifications.

### Verify MCP Tool Status

After adding an MCP action, verify its status in the action list:

- Tool name, description, and server details
- Input parameters sent to the tool
- Output returned by the tool
- Execution state (Success or Failure)
- Latency (in milliseconds)
- Server name and ID
- Transaction ID

### Limitations

- **Group-level access control is not supported.** MCP tool access is managed at the organization level only.
- **MCP actions are read-only once created** in AI Agent Studio. To update an action, create a new one.
- **OAuth 2.0 Authorization Code authentication is not currently supported for MCP actions in AI Agent Studio.** Tools that use this flow can be registered as Agentic Apps, but they are not available for selection as AI Agent actions.
- **Maximum number of actions per agent** is defined by your organization's configuration. Contact your administrator for details.
