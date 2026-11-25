---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-troubleshooting-apis
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Start by isolating the problem
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-troubleshooting-apis). [Full Markdown](../../../../docs/webex-connect-troubleshooting-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this checklist to diagnose common failures when calling Webex Connect APIs.

## Selected section

## Start by isolating the problem

1. Reproduce the issue with the smallest valid request in **Try Out** on the exact API Reference operation.
2. Compare the method, path, endpoint, headers, query parameters, and request body with the operation definition.
3. Record the HTTP status, response body, `transid`, optional `trackingid`, and timestamp.
4. Confirm that the user can access the organization and has permission to perform the requested operation.
