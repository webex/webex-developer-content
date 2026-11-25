---
type: Excerpt
canonical_url: https://developer.webex.com/docs/partner-usage
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
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
