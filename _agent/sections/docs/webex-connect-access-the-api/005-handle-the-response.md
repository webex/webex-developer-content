---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-access-the-api
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle the response
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-access-the-api). [Full Markdown](../../../../docs/webex-connect-access-the-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use a Webex personal access token to call the digital asset onboarding APIs for Email, Live Chat, and In-App assets.

## Selected section

## Handle the response

A successful response confirms that the requested asset operation completed. Validate the returned asset details before storing the result. For a failed request, use the HTTP status, response `code`, `description`, and `transid` to identify the cause.
