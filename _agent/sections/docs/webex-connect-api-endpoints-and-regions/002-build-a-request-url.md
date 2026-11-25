---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Build a request URL
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-api-endpoints-and-regions). [Full Markdown](../../../../docs/webex-connect-api-endpoints-and-regions.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use the API base URL associated with the API family and the region in which your organization is hosted.

## Selected section

## Build a request URL

Combine the base URL shown in the API Reference with the operation path. For example, the Email create operation uses this path:

```text
<digital-channel-onboarding-api-base-url>/v2/digital/app?channel=email
```

Use HTTPS and preserve the host, API version, path, and channel value exactly as documented.
