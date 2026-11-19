---
type: Guide
title: Become a BYOVA Provider on Webex App Hub
display_title: Become a BYOVA Provider on Webex App Hub
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
content_type: documentation
product_group:
- webex-contact-center
categories:
- app-hub
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/become-a-byova-provider)

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Overview

[Bring Your Own Virtual Agent (BYOVA)](https://developer.webex.com/docs/bring-your-own-virtual-agent)
lets your service receive Contact Center audio and conversation events through a
secure, Webex-managed data-source connection. As a provider, you publish one
[Contact Center Service App](https://developer.webex.com/docs/contact-center-service-apps) and onboard
each customer organization separately.

Your service owns secure connectivity and gateway operations. Each customer
controls authorization, virtual-agent configuration, and call routing in their
Contact Center organization.

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

## Prepare the virtual-agent gateway

Service App authorization and datasource registration let Webex Contact Center
reach your service; they do not prove that the service can handle a customer
conversation. Complete the applicable protocol implementation before asking a
customer to configure a feature or flow.

For a gRPC provider, Webex Contact Center is the gRPC client and your gateway
is the gRPC server. Implement `ProcessCallerInput` for the conversation stream
and `ListVirtualAgents` for agent discovery. Return the real, customer-eligible
agent catalog rather than an empty default response. Also implement the gRPC
health service used by Cisco ping tests and return `SERVING` or `NOT_SERVING`.
See [BYOVA over gRPC](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc) for the
protocol, JWS/JWT validation, and end-to-end gateway checks. For a WebSocket
implementation, use [BYOVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket).
For optional transport-layer client authentication on a gRPC endpoint, see
[mTLS authentication](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication);
it does not replace JWS/JWT validation.

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

## Verify the integration

Test the complete path with the customer after the feature and flow are
published:

1. Confirm that the datasource is active and belongs to the intended
   organization.
1. Confirm that the selected Service App and datasource ID match your
   onboarding record.
1. For a gRPC gateway, confirm that `ListVirtualAgents` returns the expected
   customer-eligible catalog and that Flow Designer can discover and invoke the
   selected virtual agent.
1. Confirm that Webex reaches the gateway and that the gateway validates the
   signed request for the expected organization.
1. Test a caller's conversation, error handling, and any transfer or fallback
   path.

A direct gateway health check or `grpcurl` test is not sufficient. The
meaningful test is the full path from Flow Designer through Contact Center
configuration and datasource resolution to your gateway.
Use the [BYOVA overview](https://developer.webex.com/docs/bring-your-own-virtual-agent) and the selected
protocol guide to validate the feature, flow, and gateway configuration
together.

## Handle deauthorization and offboarding

When Webex sends a [`serviceApp.deauthorized`
event](https://developer.webex.com/docs/webhooks), first verify the signature over the
unmodified raw request body. Before offboarding, require the expected resource
and event, confirm that `data.id` equals the expected Service App ID, and
verify that `data.authorizerOrgId` maps to an active onboarding record. Then:

1. Disable the organization route at your gateway immediately.
1. Mark the datasource and onboarding record inactive.
1. Remove or cryptographically erase stored organization tokens.
1. Tell the customer to remove or redirect the related Virtual Agent feature
   and flow.
1. Retain only the minimum audit information your support and compliance
   requirements need.

Do not allow a stale or deauthorized organization to continue using your
gateway.

## Provider and customer responsibilities

| Provider | Customer |
| --- | --- |
| Publishes and operates the App Hub Service App and its token-management path | Reviews scopes and authorizes the Service App |
| Operates the secure BYOVA gateway | Confirms BYOVA is available in the Contact Center organization |
| Creates, renews, and monitors the organization datasource | Creates the Virtual Agent feature |
| Provides the datasource ID and flow template | Binds the feature to a Flow Designer flow |
| Disables access after deauthorization | Publishes, routes, and tests call behavior |
