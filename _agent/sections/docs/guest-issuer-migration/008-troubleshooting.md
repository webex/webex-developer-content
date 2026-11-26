---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Troubleshooting

Errors use the standard Webex API error format with `message` and `trackingId` fields.

| HTTP status          | Typical cause                                                             | What to do                                                                                                                                                                                      |
| -------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `400 Bad Request`    | Missing or invalid `guestIssuerId`                                        | Send the `id` from `GET /v1/jwt` in the request body                                                                                                                                            |
| `400 Bad Request`    | Target is not a Service App                                               | Verify `applicationId` refers to a Service App                                                                                                                                                  |
| `403 Forbidden`      | Guest Issuer migration is not enabled                                     | Contact [Webex support](https://developer.webex.com/support) or your account team                                                                                                                                          |
| `403 Forbidden`      | Service App missing `guest-issuer:write`                                  | Recreate or update the Service App scopes                                                                                                                                                       |
| `403 Forbidden`      | Guest issuer not eligible for this org                                    | Use an issuer created by your organization                                                                                                                                                      |
| `403 Forbidden`      | Caller is not an org admin or app not authorized                          | Authorize the app with a Full Admin token first                                                                                                                                                 |
| `404 Not Found`      | Issuer does not exist                                                     | Re-check `guestIssuerId` from the list response                                                                                                                                                 |
| `409 Conflict`       | Binding already exists                                                    | Do not call bind again; contact support if the wrong app is bound                                                                                                                               |
| `200 OK` (premature) | `POST /v1/guests/token` succeeded before `bindGuestIssuer` returned `204` | The Service App may have auto-created its own guest issuer. Check `GET /v1/guests/count`; if it is greater than `0` before binding, create a **new** Service App, authorize, bind, then migrate |
| —                    | Guest token `id` does not match legacy guest users after bind             | You likely issued Service App guest tokens before binding. Create a **new** Service App, authorize, bind first, then re-issue tokens for migrated subjects                                      |
