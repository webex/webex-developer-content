---
type: Guide
title: Choose Your App Hub App Type
display_title: Choose Your App Hub App Type
canonical_url: https://developer.webex.com/docs/choose-your-app-hub-app-type
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- app-hub
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/choose-your-app-hub-app-type)

Choose the Webex app type that fits your customer workflow, then follow its development and App Hub submission guidance.

## Start with the customer workflow

Before registering an app, decide where customers will use it, whose identity it needs, and who will authorize access. App Hub helps customers discover your app; the app type determines how it runs and obtains permission.

You can combine app types when the workflow requires it. For example, an embedded app can use an OAuth integration for access to Webex APIs. Register the components you need, then check the [multiple submission guidelines](https://developer.webex.com/docs/app-hub-submission-process#multiple-submission-guidelines) before planning separate listings.

## Compare app types

| App type | Choose it when | Identity and authorization | Start building |
| --- | --- | --- | --- |
| OAuth integration | Your application needs to call Webex APIs on behalf of a signed-in user. | The user grants consent for the requested scopes. Access is also subject to the customer's organization policies. | [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) |
| Service App | Your application needs ongoing, organization-level API access that is independent of an individual user's lifecycle. | A customer administrator authorizes the app. API calls use a machine account in the authorizing organization. | [Service Apps](https://developer.webex.com/docs/service-apps); for Contact Center, [Contact Center Service Apps](https://developer.webex.com/docs/contact-center-service-apps) |
| Bot | Customers need to message your application, add it to spaces, or receive notifications from it. | The bot has its own identity. Its access differs from a user's access; it does not act as that user. | [Bots](https://developer.webex.com/docs/bots) |
| Embedded app | Customers should interact with your web application inside Webex meetings, spaces, or the sidebar. | The Embedded Apps Framework provides context and permitted user information. Use an integration separately if your workflow needs user-authorized API access. | [Embedded Apps](https://developer.webex.com/docs/embedded-apps) and [Developer Guide](https://developer.webex.com/docs/embedded-apps-guide) |
| Workspace integration | Your service needs to work with workspaces and Webex devices through the workspace integration framework. | An administrator activates the integration in Control Hub. It uses a machine account and supports granular device access. | [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations) |
| Agentic app | You want customers to discover and enable your MCP server or A2A agent. | Registration records the server's authentication configuration. Customer administrators review and enable its use. Follow the guide for the selected protocol. | [Onboard Your MCP Server](https://developer.webex.com/docs/onboard-your-mcp-server) or [Onboard Your Agent](https://developer.webex.com/docs/onboard-your-agent) |

For A2A registration, check the [Onboard Your Agent prerequisites](https://developer.webex.com/docs/onboard-your-agent#prerequisites), including beta enrollment, before planning customer availability.

## Match listing and authorization to your app

App registration, App Hub publication, and customer authorization are separate steps. Use the requirements for your app type:

- **OAuth integrations:** Register the integration and implement OAuth consent. An App Hub listing provides discovery; it does not replace user consent or override an organization's integration controls.
- **Service Apps:** To request authorization in a non-affiliated organization, follow the App Hub submission and review path described in [Service Apps](https://developer.webex.com/docs/service-apps). Listing alone does not authorize the app for a customer.
- **Bots:** Implement and test the bot's user interaction before submitting. Check the submission rules if the bot also depends on an integration.
- **Embedded apps:** Complete the [Submission Checklist for Embedded Apps](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps) and the design guidance for each supported context.
- **Workspace integrations:** Follow the public integration onboarding process in [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations). Its Control Hub activation and deployment process has its own requirements.
- **Agentic apps:** Follow [Submit to App Hub & Badging](https://developer.webex.com/docs/agentic-apps-app-hub), then give customers the [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps).

## Choose a path for BYOVA

If you provide a virtual agent for Webex Contact Center customers, start with [Become a BYOVA Provider](https://developer.webex.com/docs/become-a-byova-provider). It connects Service App authorization, provider provisioning, customer configuration, and offboarding into one workflow.

Use the protocol guides linked from that article for implementation details. Keep provider responsibilities separate from the configuration that a customer administrator performs.

## Test before submitting

Choose a sandbox for the product your app supports:

- **Webex Suite:** Use the [Suite Sandbox](https://developer.webex.com/app-hub/docs/developer-sandbox-guide) for supported collaboration workflows.
- **Webex Contact Center:** Use the [Contact Center Sandbox](https://developer.webex.com/app-hub/docs/sandbox_cc) guide to set up a licensed Contact Center test environment with administrator access and preconfigured resources. For virtual agent solutions, also confirm the prerequisites in the [BYOVA provider guide](https://developer.webex.com/app-hub/docs/become-a-byova-provider).

Check the selected sandbox's prerequisites and available features; a sandbox does not establish that every API or app type is available.

Verify the complete customer journey:

1. A new customer can understand what the app does and what accounts or licenses it requires.
2. The intended user or administrator can authorize it with only the permissions it needs.
3. The main workflow works in each supported Webex context.
4. Denied access, expired credentials, and interrupted setup produce a useful recovery path.
5. Customers can stop using the app and follow the applicable deauthorization or removal procedure.

Use separate test identities where the workflow has different roles. A successful test inside your own organization does not prove that authorization in an unrelated customer organization is ready.

## Prepare your listing

Follow [Submit Your App](https://developer.webex.com/docs/app-hub-submission-process) for review, listing materials, and submission requirements. Describe the customer outcome, required accounts, setup steps, support contact, and requested permissions clearly.

After approval, continue with [Manage Your Published App](https://developer.webex.com/docs/manage-your-published-app).
