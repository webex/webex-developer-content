---
type: Excerpt
canonical_url: https://developer.webex.com/docs/authentication
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you implement OAuth
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/authentication). [Full Markdown](../../../../docs/authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Why authentication is required](001-why-authentication-is-required.md) [Requesting Permission](003-requesting-permission.md)

## Article introduction

Webex authentication lets your integration securely access Webex APIs on behalf of a user without collecting or storing their Webex password.

## Selected section

## Before you implement OAuth

To implement the OAuth flow described below, you need:

- A registered [Webex integration](https://developer.webex.com/docs/integrations) and its client ID and client secret.
- A redirect URI that exactly matches one of the URIs registered for the integration.
- The minimum [integration scopes](https://developer.webex.com/docs/integration-scopes) required by your application.
- A server that can receive the OAuth callback and protect the client secret and tokens.

For Webex Contact Center administrator APIs, the user authorizing the integration must use a Webex account backed by Cisco Webex Common Identity and have the appropriate administrator role in Control Hub. See [Webex Contact Center administrator roles and privileges](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges).
