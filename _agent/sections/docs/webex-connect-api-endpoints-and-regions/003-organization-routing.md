---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Organization routing
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions). [Full Markdown](../../../../docs/webex-connect-api-endpoints-and-regions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the API base URL associated with the API family and the region in which your organization is hosted.

## Selected section

## Organization routing

Digital Channel Onboarding requests require the organization identifier in the `x-organization-id` header:

```http
x-organization-id: <organization-id>
```
