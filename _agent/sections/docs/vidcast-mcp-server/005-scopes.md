---
type: Excerpt
canonical_url: https://developer.webex.com/docs/vidcast-mcp-server
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/vidcast-mcp-server). [Full Markdown](../../../../docs/vidcast-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](004-authentication.md)

## Selected section

## Scopes

3 OAuth scopes required:

| Scope | Description |
|-------|-------------|
| `spark:mcp` | Required for MCP server connection |
| `Identity:Organization` | Access to organization-level identity information |
| `Identity:Config` | Access to identity configuration |

**Full scope string:**

```sh
spark:mcp Identity:Organization Identity:Config
```
