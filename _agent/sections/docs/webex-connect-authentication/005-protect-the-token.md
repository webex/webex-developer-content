---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Protect the token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-authentication). [Full Markdown](../../../../docs/webex-connect-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use a Webex personal access token to authenticate requests to the digital asset APIs for Email and Chat assets. Chat assets support Push Notifications, Live Chat, and In-App Messaging.

## Selected section

## Protect the token

- Do not commit personal access tokens to source control.
- Do not include personal access tokens in browser code, screenshots, or support tickets.
- Remove the `Authorization` header and token values from application logs.
- Obtain a new token after the current token expires.
- Request only the scopes needed for the asset operations you are testing.
