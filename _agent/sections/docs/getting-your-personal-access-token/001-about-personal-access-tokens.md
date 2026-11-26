---
type: Excerpt
canonical_url: https://developer.webex.com/docs/getting-your-personal-access-token
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- About personal access tokens
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/getting-your-personal-access-token). [Full Markdown](../../../../docs/getting-your-personal-access-token.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Learn how to get a personal access token for testing Webex APIs with your own account.

## Selected section

## About personal access tokens

Webex REST API requests must include an API access token in the request's `Authorization` header. The token must have the data access scopes required by the requested resource. In a production app, you create a [Webex Integration](https://developer.webex.com/docs/integrations) and use OAuth to obtain an access token. For testing purposes, however, you can get a personal access token from the Developer Portal to make API calls on your own behalf.

Notes about personal access tokens:

* They should not be used in production apps. Instead, create an [Integration](https://developer.webex.com/docs/integrations) with the desired access scopes to obtain access tokens.
* Personal access tokens are valid for 12 hours after logging into the Developer Portal.
