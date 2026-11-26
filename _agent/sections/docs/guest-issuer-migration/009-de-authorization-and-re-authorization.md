---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- De-authorization and Re-authorization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## De-authorization and Re-authorization

`bindGuestIssuer` is a **one-time** setup step. If an org admin removes and later restores Service App authorization, the guest issuer binding **remains**.

- **Do not** call `bindGuestIssuer` again after re-authorization—a second bind returns `409 Conflict`.
- After re-authorization, exchange Service App credentials for a **new** access token, then continue using `POST /v1/guests/token`.
- Guest users and the guest issuer organization are unchanged across de-authorization and re-authorization.

A guest issuer binding **cannot be transferred** to a different Service App through the public API. If you must use a different Service App with the same guest issuer, contact [Webex support](https://developer.webex.com/support).
