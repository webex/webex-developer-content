---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-troubleshooting-apis
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- The request is limited
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-troubleshooting-apis). [Full Markdown](../../../../docs/webex-connect-troubleshooting-apis.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use this checklist to diagnose common failures when calling Webex Connect APIs.

## Selected section

## The request is limited

- Reduce the request rate and review the limits documented for the API family and operation.
- Avoid concurrent updates to the same resource.
- Before repeating a create or update request, verify whether the earlier request succeeded.
