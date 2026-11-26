---
type: Excerpt
canonical_url: https://developer.webex.com/docs/provisioning-on-control-hub
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Refreshing MCP Server Tools in Control Hub
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/provisioning-on-control-hub). [Full Markdown](../../../../docs/provisioning-on-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](003-authentication.md)

## Article introduction

Use the [Webex Control Hub](https://admin.webex.com/) to provision Agentic Apps for your organization. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.

---



> **Info**
>
> Users acknowledge and agree that they bear full responsibility for understanding, complying with, and managing all aspects of the liability framework related to their use of MCP applications.





> **Info**
>
> This guide is for administrators only. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.

## Selected section

## Refreshing MCP Server Tools in Control Hub

The backend caches each MCP server's tool list for up to one hour. During this period, requests from Control Hub administrators or SDK clients return the cached list. After the cache expires, the next backend request retrieves the latest tools from the MCP server.
