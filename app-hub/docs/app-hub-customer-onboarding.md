---
type: Guide
title: Plan Customer Setup and Authorization
display_title: Plan Customer Setup and Authorization
canonical_url: https://developer.webex.com/docs/app-hub-customer-onboarding
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- app-hub
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/app-hub-customer-onboarding)

Help customers connect your App Hub app by separating developer preparation from customer authorization, configuration, and verification.

## Who this guide is for

This guide is for App Hub Developers preparing customer-facing setup instructions. Before you begin, [choose your app type](https://developer.webex.com/docs/choose-your-app-hub-app-type), identify the Webex products your app uses, and check the prerequisites in its development guide.

If you are a customer administrator installing an existing app, start with the developer's setup instructions and the app-type guidance below. You do not need to create a replacement app registration for the developer's app.

App registration, App Hub publication, and customer authorization are separate steps. An App Hub listing does not grant access to a customer's organization or replace its application policies.

## Agree on responsibilities

| App developer | Customer |
| --- | --- |
| Operate the application and maintain its registration, listing, and support contact. | Identify the users and administrators who will approve and use the app. |
| Explain supported products, required accounts or licenses, requested permissions, and data use. | Confirm product access and review permissions against organization policies. |
| Provide setup instructions and a way to verify the customer connection. | Complete the applicable authorization and product configuration steps. |
| Support failed setup, credential recovery, and offboarding. | Test the intended workflow and follow the removal instructions when access is no longer needed. |

Keep developer-owned client secrets and customer access tokens in your service's approved secrets store. Do not ask customers to send these credentials through email, chat, or a support ticket.

## Match authorization to the app

| App or solution | Customer handoff | Detailed guidance |
| --- | --- | --- |
| OAuth integration | The user signs in and consents to the requested scopes, subject to organization policies. | [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) |
| Service App | A customer Full Admin reviews and authorizes the app. The developer then obtains credentials for that authorizing organization. Follow the documented App Hub submission path before requesting authorization in a non-affiliated organization. | [Service Apps](https://developer.webex.com/docs/service-apps) |
| BYOVA solution | The customer authorizes the provider's Service App and configures Contact Center. The provider handles its customer-specific onboarding and datasource connection. | [BYOVA provider guide](https://developer.webex.com/docs/become-a-byova-provider) |
| Embedded app | Explain the supported meetings, spaces, or sidebar context and applicable organization controls. If the app also uses an OAuth integration, explain that separate consent step. | [Embedded Apps developer guide](https://developer.webex.com/docs/embedded-apps-guide) |
| Bot | Explain how to find or add the bot and start its supported interaction. If your solution also uses an integration, document its separate authorization step. | [Bots](https://developer.webex.com/docs/bots) |
| Workspace integration | A customer administrator activates the integration in Control Hub and reviews its device access. | [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations) |
| Agentic app | Provide the server information and usage instructions the customer administrator needs for review and enablement. Check availability and prerequisites for the chosen protocol. | [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps) |

BYOVA is a solution journey built on a Service App and Contact Center configuration, rather than a separate app registration type. Service App authorization alone does not configure call routing.

## Write the customer setup instructions

Provide these details before asking a customer to authorize the app:

1. **Requirements:** Supported Webex products, required accounts or licenses, and the role needed for each step.
2. **Permissions and data:** What access the app requests, why it needs that access, and where customers can review privacy and support information.
3. **Setup sequence:** Separate actions in your application from actions in Webex. Identify when the customer should hand the task to an administrator.
4. **Success check:** Name the expected connection state and a small task that proves the customer's intended workflow works.
5. **Recovery and removal:** Explain how to retry interrupted setup, obtain help, and stop using the app.

Link to the app-type guide for detailed platform procedures. Keep your own instructions focused on your app's configuration and customer outcome.

## Verify the customer journey

Test with the intended customer roles and organization arrangement. Success inside the developer's organization does not establish that authorization in a non-affiliated customer organization works.

Confirm that the customer can authorize the intended app, complete product configuration, and perform the main workflow. Where the app serves multiple organizations, verify that each connection uses the correct customer's authorization and data.

Also test denied authorization, insufficient permissions, expired credentials, and interrupted setup. Show a useful next step and preserve enough non-sensitive context for support. For BYOVA, follow the provider guide's end-to-end call verification, rather than treating authorization as proof that calls will reach the virtual agent.

## Plan changes and offboarding

Explain how customers revoke or deactivate access using the procedure for their app type. Coordinate that action with disabling the customer connection in your service and handling retained data according to your published policy. Do not promise that revocation immediately invalidates every previously issued credential unless the relevant platform contract establishes that behavior.

Continue with [Manage Your Published App](https://developer.webex.com/docs/manage-your-published-app) for listing changes, support, ownership changes, and retirement.
