---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Bind a Guest Issuer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Bind a Guest Issuer

An org admin binds the legacy guest issuer to the authorized Service App. This is a **migration-only**, one-time call.

```bash
curl --request POST \
  --header "Authorization: Bearer ORG_ADMIN_ACCESS_TOKEN" \
  --header "Content-Type: application/json" \
  --data '{"guestIssuerId": "GUEST_ISSUER_ID_FROM_LIST"}' \
  https://webexapis.com/v1/applications/SERVICE_APP_ID/bindGuestIssuer
```

| Item               | Detail                                                             |
| ------------------ | ------------------------------------------------------------------ |
| **Method**         | `POST`                                                             |
| **Endpoint**       | `/v1/applications/{applicationId}/bindGuestIssuer`                 |
| **Caller**         | Webex organization administrator (human user)                      |
| **Token**          | Org admin OAuth access token with `spark-admin:applications_write` |
| **Path parameter** | `applicationId` — your Service App ID (`SERVICE_APP_ID`)           |
| **Request body**   | `guestIssuerId` — the `id` from `GET /v1/jwt`                      |
| **Success**        | `204 No Content` (empty body)                                      |

The Service App machine account token, bot tokens, and personal developer tokens (without org admin role) are **not** valid for this call.
