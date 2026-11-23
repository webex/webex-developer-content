---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- After Migration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## After Migration

After `bindGuestIssuer` succeeds, update your legacy integration to stop generating shared-secret JWTs and instead issue guest tokens through `POST /v1/guests/token` using the Service App access token, as documented in [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management).



> **Do not use the legacy JWT flow after bind**
>
> After `bindGuestIssuer` succeeds, the legacy shared secret for that guest issuer is disabled. Do not continue using the legacy JWT login flow for that issuer. From that point forward, issue guest tokens only with `POST /v1/guests/token` using the Service App access token.



Guest users and history associated with the bound issuer organization are preserved through the migration when you complete the bind **before** issuing any Service App guest tokens.
