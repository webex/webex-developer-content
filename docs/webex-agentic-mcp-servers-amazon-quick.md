---
type: Guide
title: Webex MCP Server Usage Guide | Amazon Quick
display_title: Amazon Quick
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick)

---

Connect Amazon Quick to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Prerequisites

- An **Amazon Quick Enterprise** subscription
- Admin access to the Amazon Quick console
- The Webex MCP server URL you want to connect to

## Set Up the MCP Integration

### 1. Open the Integrations Console

1. Sign in to the [Amazon Quick console](https://quicksight.aws.amazon.com)
2. In the left navigation, choose **Integrations**
3. Choose **Add**

### 2. Enter Server Details

On the **Create Integration** page, fill in the following:

- **Name** — A descriptive name for your integration (e.g., `My Webex Meeting`) — this can be anything
- **Description** (optional) — Any text describing the integration's purpose
- **MCP server endpoint** — The full URL of the Webex MCP server (must start with `https://`)

Choose **Next**.

### 3. Configure Authentication

Select **User authentication (OAuth)** and provide the following credentials:

You'll get the Client ID and Client Secret from your [Webex OAuth 2.0 Integration](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20)

- **Client ID** — The Client ID from your Webex Integration
- **Client Secret** — The Client Secret from your Webex Integration
- **Token URL** — `https://webexapis.com/v1/access_token`
- **Authorization URL** — `https://webexapis.com/v1/authorize`
- **Redirect URL** — The callback URL will be displayed by Amazon Quick after you select the authentication method

> When creating your Webex Integration, use the **Redirect URL** shown in this step as the callback URL.

Choose **Create and continue**.

### 4. Review and Enable Tools

Amazon Quick connects to the Webex MCP server and automatically discovers the available tools. Review the list of discovered actions and enable the ones you want to use.

Choose **Next**, then optionally share the integration with other users in your organization.

## Resources

- [Amazon Quick Official Documentation](https://docs.aws.amazon.com/quick/latest/userguide/mcp-integration.html)
