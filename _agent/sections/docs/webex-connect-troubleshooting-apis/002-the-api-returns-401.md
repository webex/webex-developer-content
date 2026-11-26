---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-troubleshooting-apis
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- The API returns 401
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-troubleshooting-apis). [Full Markdown](../../../../docs/webex-connect-troubleshooting-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this checklist to diagnose common failures when calling Webex Connect APIs.

## Selected section

## The API returns 401

- Confirm that the request includes the authentication credentials required by the API.
- If the API uses a bearer token, obtain a current token if it has expired.
- Ensure that credentials are complete, correctly formatted, and sent in the required header.
