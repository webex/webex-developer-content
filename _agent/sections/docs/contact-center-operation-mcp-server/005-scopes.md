---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server). [Full Markdown](../../../../docs/contact-center-operation-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

## Scopes

4 OAuth scopes required:

| Scope | Description |
|-------|-------------|
| `spark:mcp` | Required to connect through the Webex MCP server platform. |
| `cjp:config_read` | Read access to Webex Contact Center configuration and reporting-related APIs. |
| `spark:people_read` | Read access to Webex identity information used for organization and agent resolution. |
| `cjp:user` | Required for selected Virtual Agent insight APIs, including VA transcript and VA summary access. |

**Full scope string:**

```sh
spark:mcp cjp:config_read spark:people_read cjp:user
```
