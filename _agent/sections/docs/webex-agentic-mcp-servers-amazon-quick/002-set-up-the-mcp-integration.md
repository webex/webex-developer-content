---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Set Up the MCP Integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-agentic-mcp-servers-amazon-quick). [Full Markdown](../../../../docs/webex-agentic-mcp-servers-amazon-quick.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

Connect Amazon Quick to a Webex MCP server.

> Before configuring, you'll need OAuth 2.0 credentials. See [OAuth 2.0 setup instructions](https://developer.webex.com/docs/webex-agentic-mcp-servers#2-oauth-20) in the main guide.

## Selected section

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
