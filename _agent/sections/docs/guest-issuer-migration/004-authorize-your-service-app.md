---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-issuer-migration
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize Your Service App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-issuer-migration). [Full Markdown](../../../../docs/guest-issuer-migration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](002-before-you-begin.md) [De-authorization and Re-authorization](009-de-authorization-and-re-authorization.md)

## Article introduction

Migrate an existing legacy Guest Issuer application to [Service App Guest Management](https://developer.webex.com/docs/sa-guest-management) by binding your guest issuer to a Service App before you issue guest tokens.

## Selected section

## Authorize Your Service App

Before you bind, a Webex organization **Full Admin** must authorize the Service App for your organization in Control Hub.

1. In the [developer portal](https://developer.webex.com), the Service App developer clicks **Request Admin Authorization** on the Service App details page so the app appears in the organization's Control Hub. If you are a Full Admin in your own org, you can skip this step and authorize the app directly.
2. The Full Admin logs in to [Control Hub](https://admin.webex.com), opens **Management** > **Apps** > **Service Apps**, selects the Service App, and reviews its description and requested scopes.
3. The admin clicks **Authorize**, then **Save**.

If the Service App does not appear in Control Hub, ask the developer to submit it for admin authorization first. For Service App creation, scopes, and the full developer and admin flows, see [Using Webex Service Apps](https://developer.webex.com/docs/service-apps).
