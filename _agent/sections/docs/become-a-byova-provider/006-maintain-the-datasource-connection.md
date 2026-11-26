---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Maintain the datasource connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Maintain the datasource connection

Datasource registration is not a one-time operation. It creates the short-lived
[JWS information](https://developer.webex.com/create/docs/bring-your-own-datasource) Webex uses when
connecting to your gateway. Before the datasource credential expires, update
the datasource with a fresh nonce and renewed token lifetime. Webex does not
attempt an outbound request for an expired datasource credential.

Run a per-organization reconciliation job that:

- Refreshes the provider Integration access token from its stored refresh
  token, then refreshes each customer Service App access token when necessary.
- Renews datasource credentials before expiry.
- Detects a missing, disabled, or drifted datasource.
- Monitors each Service App authorization webhook. After correcting a delivery
  failure, [reactivates a disabled subscription](https://developer.webex.com/docs/webhooks#disabled-webhooks)
  and reconciles Developer Portal organization authorizations with onboarding
  records to recover missed events.
- Alerts your operations team before a customer's connection expires.
- Does not overwrite customer Contact Center configuration.
