---
type: Article
title: Simplify MCP Authentication with Webex Service Apps
canonical_url: https://developer.webex.com/blog/simplify-mcp-authentication-with-webex-service-apps
content_type: blog
date: '2026-10-31'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/simplify-mcp-authentication-with-webex-service-apps)

An AI agent needs an authorized connection before it can use Webex tools. Webex Service App authentication gives eligible Webex-hosted MCP servers an organization-level identity, with access approved by a Full Administrator in Control Hub. During setup, developers and administrators do not need to enter a client ID, client secret, or access token.

Here is how the Developer Portal and Control Hub fit together, and what to check before you start using an enabled tool.

### An identity for your organization's workflows

Some automations need to operate on behalf of an organization. Think of an assistant that retrieves approved operational information for a support workflow, rather than relying on one employee to keep the connection authorized.

[Webex Service Apps](https://developer.webex.com/docs/service-apps) support that model through a machine identity in the authorizing organization. The associated permissions come from the Service App's authorization and scopes. This does not give an agent unrestricted access to Webex data: the requested scopes and the requirements of each API still matter.

For MCP, the Developer Portal brings this authentication choice into agentic app configuration. It is available for **eligible Webex-hosted MCP servers**. Check the options offered for your server's URL when registering or editing the app.

### Configure the agentic app in the Developer Portal

Start with the [MCP server onboarding guide](https://developer.webex.com/docs/onboard-your-mcp-server). In the agentic app registration form:

1. Enter the eligible Webex-hosted MCP server URL and the app's other required details.
2. Select **Webex Service App** from the available authentication methods. The option appears after an eligible URL is entered.
3. Complete registration. After provisioning succeeds, the details page displays the **Associated Webex Service App ID**.

![Developer Portal agentic app authentication selector with Webex Service App selected.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5133c58ff5f23245/6ae824c1073e0e14b00765c3/devportal-service-app-auth.png)

*Select Webex Service App when configuring an eligible MCP server in the Developer Portal.*

That association connects the MCP app configuration to the Service App that an administrator will authorize. Each customer organization must grant its own authorization.

### Review and authorize in Control Hub

A Full Administrator completes the organization setup:

1. Open **Apps > Agentic Apps** and select the MCP server.
2. Review the app's access policy and enable the tools your organization needs.
3. On **Authentication**, select **Webex Service App** as the active method.
4. Follow the associated **Service Apps page** link.
5. Review the Service App and its requested scopes, then authorize it and save.

![Control Hub Authentication panel showing Webex Service App selected, the associated Service App name and ID, and a link to the Service Apps page.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5d5bf245ea1458d2/6ae824cfe3c2e84028333073/control-hub-service-app-auth.png)

*Control Hub identifies the associated Service App and links to its authorization page.*

Selecting the authentication method and allowing the agentic app do not complete the Service App grant. The Full Admin authorization is a separate step.

The [Control Hub provisioning guide](https://developer.webex.com/docs/provisioning-on-control-hub#webex-service-app) covers the authentication settings, and the [Service Apps guide](https://developer.webex.com/docs/service-apps#full-admin-authorization-of-a-service-app) explains the administrator's authorization flow.

### Make the first test small

Once configuration and authorization are complete, test an enabled read-only tool through a client that supports your intended authentication flow. Choose a request with a small, predictable result before trying a larger workflow.

For example, a Contact Center flow assistant could start by retrieving the definition of one activity, such as Play Message. A successful test should show both the tool invocation and its returned result. That gives you a clearer check than a connected status or a conversational response alone.

Use that first result to confirm the target organization and the operation the app can perform. Then expand the test to the rest of your workflow.

### Keep authorization aligned with the app

The initial approval is only part of the lifecycle. If the Service App's requested scopes change, a Full Administrator must review and reauthorize them. Control Hub indicates when this review is required.

Continue reviewing tool availability separately. Enabling a tool controls whether it is available through the agentic app; the Service App grant controls its authorized API access. Both settings need to match the workflow you intend to run.

### Get started

Choose an eligible Webex-hosted MCP server and follow the [onboarding guide](https://developer.webex.com/docs/onboard-your-mcp-server). Then ask your Full Administrator to complete [Service App authorization in Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub#webex-service-app).

Start with one useful tool and a small test. You can build from there with an organization-level identity and a clear administrator approval flow.
