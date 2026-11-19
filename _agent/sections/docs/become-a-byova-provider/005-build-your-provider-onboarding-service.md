---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Build your provider onboarding service
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Build your provider onboarding service

Your onboarding service turns an authorization into a customer-specific BYODS
connection. It must keep each organization isolated, even if multiple
customers use the same multi-tenant gateway hostname.

When a customer Full Admin authorizes your Service App, Webex sends the
`serviceApp` `authorized` webhook to the provider Integration. Before acting on
it, verify the signature over the unmodified raw request body, require the
expected resource and event, and confirm that `data.id` equals the expected
Service App ID. Use
`data.authorizerOrgId` as the customer organization ID; the envelope `orgId`
identifies the organization that owns the webhook, not the authorizing
customer. The event does not provide the organization token pair.

Retrieve the Service App access and refresh tokens for that customer through
the supported [application-token
flow](https://developer.webex.com/docs/contact-center-service-apps). An automated provider calls the token
endpoint with the OAuth Integration's `spark:applications_token` bearer token,
the Service App client credentials, and `data.authorizerOrgId` as the target
organization. Store the resulting token pair encrypted and scoped to that
organization only. Do not ask the customer to provide Webex credentials, and
never expose your Service App client secret in a customer setup guide or browser
application.

If your onboarding needs a human-readable organization identity, use that
customer's Service App access token to call [Get Organization
Details](https://developer.webex.com/docs/api/v1/organizations/get-organization-details) for
`data.authorizerOrgId`. This requires the Service App to have been authorized
with `spark-admin:organizations_read`. Store only the returned basic identity,
such as `displayName`, that your onboarding needs. The authorization webhook
does not include an organization name, support contact, or other customer
profile details.

Then create, or safely reconcile, one [data
source](https://developer.webex.com/create/docs/bring-your-own-datasource) for that organization. Record the
datasource ID, organization ID, gateway route, credential expiry, and
provisioning status. The datasource ID is the value the customer uses when
configuring the Virtual Agent feature.
