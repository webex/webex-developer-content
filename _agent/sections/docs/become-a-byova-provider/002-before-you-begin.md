---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Before you begin

Before onboarding a customer, make sure that you have:

- A publicly reachable [BYOVA gateway](https://developer.webex.com/docs/bring-your-own-virtual-agent)
  that implements the required virtual-agent protocol and validates
  Webex-signed requests.
- A [Contact Center Service App](https://developer.webex.com/docs/contact-center-service-apps) with the
  appropriate [BYODS schema](https://developer.webex.com/create/docs/bring-your-own-datasource), approved
  data-exchange domain or domains, and the `spark-admin:datasource_read` and
  `spark-admin:datasource_write` scopes. If your onboarding records a
  human-readable customer organization name, also declare
  `spark-admin:organizations_read` on the Service App. It permits the
  Service App to read basic organization details after authorization.
- A provider-owned token-management path. For automated onboarding, use a
  separate OAuth Integration with `spark:applications_token` and
  `spark:applications_webhook_write`; it retrieves organization-specific token pairs and
  creates the Service App webhook subscriptions. Complete the [Integration
  authorization-code flow](https://developer.webex.com/docs/integrations#using-the-refresh-token), then
  securely store and refresh its token pair.
  Manual retrieval in the Developer Portal is suitable for sandbox or
  troubleshooting; a production App Hub provider must automatically register
  the datasource after authorization.
- A [Contact Center sandbox](https://developer.webex.com/docs/sandbox_cc) for end-to-end testing. Confirm
  that BYOVA is enabled and the customer has the required 3P-Virtual-Agent SKU
  for the target Contact Center organization before configuring a customer
  flow.

For general Service App concepts, see [Using Webex Service
Apps](https://developer.webex.com/docs/service-apps). For the BYODS registration, token, and JWS
contract, see [Bring Your Own Data Source](https://developer.webex.com/create/docs/bring-your-own-datasource).
