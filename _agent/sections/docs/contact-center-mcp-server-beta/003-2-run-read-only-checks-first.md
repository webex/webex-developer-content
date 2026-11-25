---
type: Excerpt
canonical_url: https://developer.webex.com/docs/contact-center-mcp-server-beta
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 2. Run read-only checks first
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/contact-center-mcp-server-beta). [Full Markdown](../../../../docs/contact-center-mcp-server-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test the Webex Contact Center MCP Server with a supported MCP client during the Webex Developer Beta. For the complete tool reference, see [Contact Center MCP Server](https://developer.webex.com/docs/contact-center-mcp-server).

## Selected section

## 2. Run read-only checks first

Run these checks before any write operation:

1. `wxcc-list-flows` — confirm that authorized flows or subflows can be listed or searched.
2. `wxcc-get-flow` — retrieve a draft, latest version, or specific flow version.
3. `wxcc-view-config` — read an authorized configuration resource such as an entry point, team, dial plan, or contact service queue.
4. `wxcc-get-activity-definitions` and `wxcc-describe-activity` — retrieve activity schemas before authoring a flow.
5. `wxcc-get-choices` — resolve organization-specific values instead of guessing IDs.

The expected result is tenant-scoped data for authorized resources only. Stop and report an authorization or data-boundary failure before continuing.
