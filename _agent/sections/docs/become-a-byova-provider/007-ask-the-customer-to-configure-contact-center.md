---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Ask the customer to configure Contact Center
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Ask the customer to configure Contact Center

Service App authorization and datasource registration do not route calls. A
customer [Contact Center administrator](https://developer.webex.com/docs/contact-center-service-apps) must
explicitly configure the Virtual Agent feature and Flow Designer flow.

Provide the customer with the datasource ID and an importable flow template,
then ask them to:

1. In Control Hub, go to **Contact Center** > **Integrations** > **Features**.
1. Create a Virtual Agent feature.
1. Select **Service App** as the connector type.
1. Select your authorized Service App.
1. Enter the datasource ID as the **Resource Identifier**, then create the
   feature.
1. Import or create a Flow Designer flow that invokes the feature.
1. Associate, publish, and test the flow for the intended entry point.

Flow activation remains a customer-owned action because it determines how
their calls are handled, transferred, and escalated. See the [BYOVA
overview](https://developer.webex.com/docs/bring-your-own-virtual-agent) for the common Contact Center
setup, and use the protocol guide for your gateway implementation. For
programmatic flow creation or import, see [Flow Orchestration
APIs](https://developer.webex.com/docs/flow-orchestration).
