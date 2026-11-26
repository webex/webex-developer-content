---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partner-usage
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Limitations and Best Practices
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/partner-usage). [Full Markdown](../../../../docs/partner-usage.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This page serves as partner specific "hints" guide for the general Webex APIs

## Selected section

## Limitations and Best Practices

Remember, you can't manage more than 2000 organizations in your list. If you add another one, a previous entry will be removed. Also, any organization added through Dynamic Patch will be removed from your list after 24 hours. To effectively manage your list, use the GET /organizations/{id} command before making API calls. If you're dealing with more than 2000 customers per day, you may need to repeat this process.
