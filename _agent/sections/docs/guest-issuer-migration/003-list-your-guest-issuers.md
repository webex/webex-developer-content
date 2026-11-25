---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- List Your Guest Issuers
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## List Your Guest Issuers

If you already created guest issuers, list them and read each item's `id`. Use that value as `guestIssuerId` when you bind.

Use the developer who originally created the legacy Guest Issuer application—the same developer account that had access when Guest Issuer apps were managed in the developer portal. That developer's personal access token must include the `spark:applications_read` scope.

### Request

```bash
curl --request GET \
  --header "Authorization: Bearer PERSONAL_ACCESS_TOKEN" \
  https://webexapis.com/v1/jwt
```

### Response

The response includes an `items` array. Each item includes `id`, `name`, and `created`. Secrets are **not** returned on the list. Pick the `id` of the issuer you want to bind and pass it as `guestIssuerId` in the bind request.

```json
{
  "items": [
    {
      "id": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMV9pbnQxMy9PUkcvZGVmNTY3ODk=",
      "name": "My Guest Issuer",
      "created": "2024-01-15T10:00:00.000Z"
    }
  ]
}
```

If `items` is empty, confirm you are using the original Guest Issuer creator's token with `spark:applications_read`. If you are starting a **new** integration without a legacy issuer, you do not need this step—see [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) instead.
