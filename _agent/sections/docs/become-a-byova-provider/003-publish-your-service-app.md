---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Publish your Service App
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Publish your Service App

Create a [Contact Center Service App](https://developer.webex.com/docs/contact-center-service-apps) in the
Webex Developer Portal and configure the following before submitting it to App
Hub:

1. Select the [data-exchange schema](https://developer.webex.com/create/docs/bring-your-own-datasource) used
   by your BYOVA gateway.
1. Add every production hostname that Webex can call. Each declared domain must
   be owned by your organization. You may use third-party hosting while testing,
   but move to a provider-owned domain before App Hub submission. Enter
   hostnames only; do not include a scheme, path, or port in the Service App
   domain configuration.
1. Request only the scopes your service needs, including the BYODS datasource
   read and write scopes. If your provider onboarding needs a human-readable
   organization name, add `spark-admin:organizations_read` to the Service App
   before customers authorize it.
1. Submit the Service App through the [Webex App Hub submission
   process](https://developer.webex.com/docs/app-hub-submission-process). After approval, it appears in
   customer Control Hub organizations for Full Admin authorization.
1. If you automate authorization onboarding, use a separate provider-owned
   OAuth Integration, registered by the same Developer Portal developer who
   created the Service App, to create [`serviceApp` webhook
   subscriptions](https://developer.webex.com/blog/webhooks-for-service-app-authorizations). Subscribe to
   both `authorized` and `deauthorized`, filter each subscription by the exact
   Service App ID, and set a webhook secret. The Service App itself, customer
   administrator, and customer-org machine account do not create or own these
   webhooks.

Choose your declared [BYODS domains](https://developer.webex.com/create/docs/bring-your-own-datasource)
carefully. A customer's authorization approves those domains, and every
datasource URL you register must belong to one of them. The datasource URL must
also match the URL that your gateway validates.
