---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-operation-mcp-server-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 4. Test configuration and routing visibility
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-operation-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-operation-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center Operation MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center Operation MCP Server](https://developer.webex.com/docs/contact-center-operation-mcp-server).

## Selected section

## 4. Test configuration and routing visibility

Use known test objects where possible. These checks read the current Contact Center configuration; they do not change it.

| Check | Operations MCP tool | What to validate |
|---|---|---|
| List flows | `wxcc-operations-list-flows` | Authorized flows and subflows can be listed or searched. |
| Read a flow | `wxcc-operations-export-flow` | A known flow can be retrieved for review. |
| Queue routing | `wxcc-operations-explain-queue-routing` | A known queue's routing settings, skill requirements, related flow references, and bounded configured-agent coverage when requested are explained. |
| Agents by skill | `wxcc-operations-get-agents-by-skill` | The response identifies configured coverage for a known skill and distinguishes configuration from current availability. |
| AI feature settings | `wxcc-operations-get-ai-features` | The response shows the tenant's configured Cisco AI Assistant feature state and scope, subject to reported coverage. |

For a queue-routing test, record the queue used and confirm that the response does not confuse an agent being logged in or available with being qualified for the queue.

### Routing pass criteria

- The requested queue, flow, skill, or feature is identified correctly.
- The response distinguishes configured settings from what happened to a live contact.
- Related flows and references are clearly labeled.
- Partial or unavailable information is identified instead of being presented as complete.
