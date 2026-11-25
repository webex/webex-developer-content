---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-access-the-api
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Provide the organization and request details
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-access-the-api). [Full Markdown](../../../../docs/webex-connect-access-the-api.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use a Webex personal access token to call the digital asset onboarding APIs for Email, Live Chat, and In-App assets.

## Selected section

## Provide the organization and request details

Include the organization ID and JSON media type where the operation requires them:

```http
x-organization-id: <organization-id>
Content-Type: application/json
```

You can also provide a unique `trackingid` header to help correlate the request during troubleshooting.

Use the exact HTTP method, path, query parameters, and request body defined for the asset operation. For example, Email asset creation uses `POST /v2/digital/app` with `channel=email`.
