---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before You Begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Before You Begin

Complete all of the following before binding. Skipping a step is a common cause of `403` or `409` errors.

### Prerequisites

- A legacy Guest Issuer application that already exists for your organization.
- A Service App created with at least `guest-issuer:write` and `guest-issuer:read` scopes. See [Using Webex Service Apps](https://developer.webex.com/docs/service-apps).
- A Webex organization **Full Admin** to authorize the Service App and perform the bind.
- The personal access token of the **developer who created the legacy Guest Issuer** (with `spark:applications_read`) to list issuers—see [List Your Guest Issuers](https://developer.webex.com/docs/guest-issuer-migration#list-your-guest-issuers) below.

On the migration path, do **not** call `POST /v1/guests/token` with the Service App until **after** `bindGuestIssuer` returns `204 No Content`. If you call `POST /v1/guests/token` before binding, the request can still return `200 OK`, but developer-applications may auto-create a **new** guest issuer for the Service App machine account instead of using your legacy issuer. That Service App can no longer be used for a clean migration to the legacy issuer.

**How to recognize this state before you bind:**

- `POST /v1/guests/token` returned `200 OK` before `bindGuestIssuer` returned `204 No Content`.
- `GET /v1/guests/count` returns a value greater than `0` before binding completes.

`bindGuestIssuer` may still return `204 No Content` even after a premature guest token call, so a successful bind does **not** mean the migration is clean. If you see either signal above, create a new Service App, authorize it, bind the legacy issuer, and only then call `POST /v1/guests/token`.
