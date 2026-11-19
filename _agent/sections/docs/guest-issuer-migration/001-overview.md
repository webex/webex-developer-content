---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Overview

This page is for **migrating** from a legacy Guest Issuer application. If you are building a **new** guest integration with no legacy Guest Issuer, use [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management)—you do not need to call `bindGuestIssuer`.

Guest Issuer applications used a shared JWT secret to create guest tokens. Service Apps use the [Guest Management API](https://developer.webex.com/admin/docs/api/v1/guest-management) instead. For organizations with an existing Guest Issuer, a one-time **bind** links that issuer to your Service App so guest tokens continue to use the same guest issuer organization.

Binding is a **one-time setup** performed by a Webex organization administrator. Your application does not call the bind API at runtime. After a successful bind, issue guest tokens with `POST /v1/guests/token` using your Service App access token—the same runtime flow described on [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management).
