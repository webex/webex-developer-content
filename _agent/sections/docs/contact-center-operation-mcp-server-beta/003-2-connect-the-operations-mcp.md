---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 2. Connect the Operations MCP
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 2. Connect the Operations MCP

1. Sign in to the Webex Developer Portal.
2. Open the [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server) page.
3. Copy the regional server URL shown for your tenant. There is no single global server URL.
4. Add the server to your supported MCP client.
5. Connect using OAuth 2.0, or use a Webex Client Identity Token (WCIT) when your MCP client supports elicitation. Clients without elicitation support must use OAuth 2.0. See [Connect Webex MCP Servers to External Clients](https://developer.webex.com/docs/webex-agentic-mcp-servers).
6. With OAuth 2.0, create or update your Webex Integration with `spark:mcp`, `cjp:config_read`, and `spark:people_read`. Add `cjp:user` only if your approved beta scope includes `wxcc-operations-get-va-summary` or `wxcc-operations-get-va-transcript`. With WCIT, the initial token includes only `spark:mcp`; clients that support elicitation request `cjp:config_read`, `spark:people_read`, and `cjp:user` only when a tool needs them.
7. Confirm that the client shows the server as connected.

If you use OAuth 2.0, record the client ID once and store the client secret only in the MCP client's secure secret storage. Never record or share a client secret, WCIT token, access token, or refresh token in screenshots, notes, or test reports.

Record the client name and version, region, date, user role, and enabled tools. Test Virtual Agent summary or transcript tools only when the organization, user, and approved beta scope allow that access.

The tools displayed by the connected beta server are the source of truth for that test environment. Tools can be enabled individually, so run only the checks for tools that are visible and approved.

### Connection pass criteria

- The regional server URL is accepted.
- Authentication completes successfully.
- The client reports the Operations MCP as connected.
- The approved Operations tools are visible.
- No unapproved write capability is presented as part of the Operations MCP test.

Stop testing and report the problem if the server cannot connect, the wrong regional URL is shown, or the available tools do not match the approved beta scope.
