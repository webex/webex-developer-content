---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Comparison with HTTP API Integrations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## Comparison with HTTP API Integrations

Workspace Integrations are _not_ the same as the integrations described in [Integrations](https://developer.webex.com/docs/integrations). They have things in common, specifically using the same underlying [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) framework, but differ in a few ways:

1. Workspace integrations are exclusively managed from Control Hub under Workspaces > Integrations.
1. The workspace integration framework was designed to support service to service interaction. The integration runs with the identity of a machine account created in the customer organization, rather than on behalf of a Webex user.
1. Workspace integrations support fine-grained access to the Webex devices xAPI and webhook or message queue change notifications for select xAPI statuses.
