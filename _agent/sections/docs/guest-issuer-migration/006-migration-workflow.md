---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Migration Workflow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Migration Workflow

| Step | Actor       | Action                                                                              | Token                                             | Success signal               |
| ---- | ----------- | ----------------------------------------------------------------------------------- | ------------------------------------------------- | ---------------------------- |
| 1    | Developer   | List guest issuers: `GET /v1/jwt`                                                   | Personal access token (`spark:applications_read`) | `items[]` with target `id`   |
| 2    | Developer   | Create Service App with `guest-issuer:read` and `guest-issuer:write`                | —                                                 | Service App in My Webex Apps |
| 3    | Org admin   | Authorize Service App in Control Hub (**Management** > **Apps** > **Service Apps**) | —                                                 | Service App authorized       |
| 4    | Org admin   | `POST /v1/applications/{id}/bindGuestIssuer`                                        | Org admin OAuth token                             | `204 No Content`             |
| 5    | Developer   | Obtain Service App access token                                                     | Service App credentials                           | Access token issued          |
| 6    | Service App | `POST /v1/guests/token`                                                             | Service App access token                          | Guest access token returned  |

Do not perform step 6 until step 4 succeeds.
