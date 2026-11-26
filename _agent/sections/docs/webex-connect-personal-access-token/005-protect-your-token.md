---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-personal-access-token
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Protect your token
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-personal-access-token). [Full Markdown](../../../../docs/webex-connect-personal-access-token.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use a Webex personal access token to call the digital asset APIs with your own user identity.

## Selected section

## Protect your token

Do not embed a personal access token in client-side code, commit it to source control, include it in screenshots, or send it in a support request. Remove the `Authorization` header from logs before sharing them.
