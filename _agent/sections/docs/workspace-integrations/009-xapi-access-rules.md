---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integrations
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- xAPI access rules
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integrations). [Full Markdown](../../../../docs/workspace-integrations.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](003-requirements.md) [Limitations](011-limitations.md)

## Article introduction

Build **Workspace Integrations** that extend the capabilities of Workspaces and Webex devices through [Webex developer APIs](https://developer.webex.com/docs/getting-started).

## Selected section

## xAPI access rules

In addition to traditional OAuth scopes, Workspace Integrations support fine grained access control for xAPI. This allows admin to inspect and approve with device APIs the integration has access to. This applies to **commands**, **events** and **statuses**. Note that for statuses, the API list both specifies which xStatus you will be able to query, and which you will receive notifications about when it changes.

It is highly recommended to specify each API directly rather than using wild cards. The fewer APIs your integration uses, the less dangerous it feels for an admin to approve it.

Note that for **xConfigurations** there are currently no such granular control, it's all or nothing based on the `spark-admin:devices_read` and`spark-admin:devices_write` scopes.

Note also that for both scopes and xAPI rules, as a developer you can set whether the requested permission is required or not. If not required, the admin may choose to not accept the optional permissions. This is typically for enhancement features that are nice to have but not strictly necessary. If you have optional permissions, you will need to check at runtime whether or not it has been accepted by the admin before using that API.
