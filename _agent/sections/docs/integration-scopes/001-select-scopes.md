---
type: Excerpt
canonical_url: https://developer.webex.com/docs/integration-scopes
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Select scopes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/integration-scopes). [Full Markdown](../../../../docs/integration-scopes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Available scopes](002-available-scopes.md) [Important scope behavior](003-important-scope-behavior.md)

## Article introduction

Use this reference to select the minimum Webex Suite and Webex Contact Center scopes that your integration needs.

## Selected section

## Select scopes

Scopes limit the resources and operations available to an access token. Select scopes when you [create an integration](https://developer.webex.com/docs/integrations), then request a space-separated subset of those registered scopes during [authentication](https://developer.webex.com/docs/authentication#requesting-permission).

The user authorizing the integration must also have permission to perform the requested operations. Granting an administrative scope does not give a non-administrator access to administrative functions.
