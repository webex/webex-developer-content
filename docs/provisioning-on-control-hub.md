---
type: Guide
title: Agentic Apps | Provisioning on Control Hub
display_title: Provisioning on Control Hub
canonical_url: https://developer.webex.com/docs/provisioning-on-control-hub
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- create
- mcp
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/provisioning-on-control-hub)

Use the [Webex Control Hub](https://admin.webex.com/) to provision Agentic Apps for your organization. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.

---



> **Info**
>
> Users acknowledge and agree that they bear full responsibility for understanding, complying with, and managing all aspects of the liability framework related to their use of MCP applications.





> **Info**
>
> This guide is for administrators only. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.



## Accessing your Agentic Apps

In Control Hub, go to **Apps → Agentic Apps**.

![Control Hub Apps Page](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt82454d503a61f12e/698aec65a788a71c4ba07c95/agentic-app-governance-guide-1.png>)
<br>

This page lists all public Agentic Apps along with the private apps which have been onboarded by users belonging to your organization.

![Control Hub Agentic Apps Page](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75c6260fc41473ab/698aec65a86c496e39a69eb4/agentic-app-governance-guide-2.png>)
<br>

## General

Select an app and open the **General** tab. Under **Access**, choose who can use the app:

- **Blocked for all users**: Block access for your organization.
- **Allowed for all users**: Allow access for your organization.
- **Limited access**: Limit discovery of an MCP server's enabled functions to users in selected groups. You can use the same groups for all functions or assign different groups per function.

Select **Save** to apply your changes. For group configuration, follow [Group-Level Access](#group-level-access).

Authorize automatic server data updates - When enabled, updates to the server's name, description, URL (within the same domain), transport type, or other metadata do not require re-authorization before they take effect. However, the admin will see an indication that changes have occurred and can re-authorize at their discretion.

### Group-Level Access

Use **Limited access** to choose which groups can discover an MCP server's enabled functions. For example, you can select a support team and a pilot group, or give individual functions different audiences. The MCP server's own authentication and authorization controls still apply when a function is invoked.

Before configuring access, make sure the groups exist in your organization. To create a Webex group, go to **Management > Groups** in Control Hub. Keep group membership aligned with the users who should have access.

#### Same groups for all functions

1. Go to **Apps > Agentic Apps**, select the MCP server, and open **General**.
2. Under **Access**, select **Limited access**.
3. Select **Same groups for all functions**.
4. Open **Search groups** and select the groups that should discover the enabled functions. Selected groups appear above the search field; remove a group with its **×** control or use **Clear All** to remove the selection.
5. Select **Save**.

![Control Hub Limited access with Support Team and Pilot Users selected for all functions.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt82fb37ddc87ef26e/6ace4078ea4b09acc937585d/agentic-limited-access-same-groups.jpg)

#### Different groups per function

1. On the MCP server's **General** tab, select **Limited access**.
2. Select **Different groups per function**, then **Save**.

![Control Hub Limited access with Different groups per function selected.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6484e0c1a6614c32/6ace40b02961026746bdc562/agentic-limited-access-per-function.jpg)

3. Open **Tools**, **Resources**, or **Prompts**, depending on the function you want to configure.
4. In the function's **Group access** column, select **Edit**. For example, select **Edit** in the **List Flows** row to configure that tool's groups.

![Control Hub Tools table with an Edit control in the Group access column for each function.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltee73d7cf12eba081/6ace4e3cd2452a39eba44934/agentic-per-function-tools-group-access.jpg)

5. On the function's **Edit group access** screen, open **Search groups** and select the groups that should discover that function.
6. Select **Save** to apply the function's group selection. Use **Cancel** to leave without saving. Repeat for each enabled function that users should be able to use.

![Edit group access for List Flows with Support Team selected and Pilot Users available in Search groups.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta345b5b22115005a/6ace4e7ddbf6ce411c0242e4/agentic-per-function-list-flows-group-picker.jpg)

In this mode, a user must belong to at least one group assigned to the function for it to appear in their enabled-function discovery. A function with no groups assigned has no matching users, even if the function is enabled. Saving an empty selection after clearing its groups removes that function from group-based discovery. Assign at least one group to every enabled function you want users to discover and use.

After saving, reopen **General** and confirm that **Limited access** and the intended group mode remain selected. For the shared-group mode, check the selected groups. For per-function assignments, return to **Tools**, **Resources**, or **Prompts**, then select the function's **Edit** control in the **Group access** column to confirm its saved groups. If **Edit** is disabled, confirm that you saved **Different groups per function** on **General** first.

Group access controls the audience; it does not enable a disabled function. Review the function's enablement settings in [Capabilities Configuration](#capabilities-configuration).

For MCP actions in [Webex AI Agent Studio](https://developer.webex.com/docs/mcp-ai-agent-studio), group-level access is not supported; tool access is managed at the organization level.

## Authentication



> **Info**
>
> Cisco official servers are automatically configured. You should update the authentication settings mentioned below only if you need to change the default authentication.



The **Authentication** section asks users for details according to the configuration set in the Developer Portal. Supported methods:

| Method | What to provide |
|--------|-----------------|
| **OAuth 2.0 – Client Credentials** | Client ID, Client Secret, Authorization Server URL, Token Endpoint Auth Method, Scope |
| **OAuth 2.0 – Authorization Code** | Client ID, Client Secret, Registration Endpoint, Authorization Endpoint, Authorization Server URL, Token Endpoint Auth Method, Scope |
| **User Token** | No input required |
| **API Key** | The API key |
| **Custom Headers** | Up to five (5) key–value pairs |
| **Webex Service App** | No credentials. Select the associated Service App and review its requested scopes. |



> **Info**
>
> For OAuth 2.0 – Client Credentials, the Token Endpoint Auth Method can be `client_secret_basic` or `client_secret_post`. For OAuth 2.0 – Authorization Code, it can be `none`, `client_secret_basic`, or `client_secret_post`.



### Webex Service App

This method is available only for eligible Webex-hosted MCP servers that offer **Webex Service App** authentication. The administrator does not enter a client ID, client secret, or token.

To select the method and review its scopes:

1. In **Apps > Agentic Apps**, select the MCP server and open the **Authentication** tab.
1. For **Authentication type**, select **Webex Service App**.
1. Select the **Service Apps page** link shown with the associated Service App.
1. Review the Service App details and requested scopes, then follow [Full Admin Authorization of a Service App](https://developer.webex.com/docs/service-apps#full-admin-authorization-of-a-service-app) to complete the separate authorization step.

If the requested scopes change later, Control Hub indicates that reauthorization is required. Review the updated scopes before reauthorizing the Service App.

![Agentic App Auth Page](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf6f108d8d67142a6/698aec650228b55116cd4021/agentic-app-governance-guide-4.png>)



> **Info**
>
> Custom Headers are configurable for all authentication types.



## Capabilities Configuration

For MCP Servers, you will see three tabs - one for **Tools**, one for **Resources** and one for **Prompts**.

![Agentic App Tools Page](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt84a91147f57b191d/698aec65a788a7015ba07c99/agentic-app-governance-guide-5.png>)
<br>

### Tools

In the Tools section you can do the following:

1. **Enable tool:** When a tool is enabled by the org admin, it becomes available to users on the client side. Users can discover and use the tool based on the access configured by the admin.
2. **Disable tool:** When a tool is disabled by the org admin, it is no longer visible or available to users on the client side. This allows admins to restrict access to tools that should not be used within the organization.
3. **Signature change:** When enabled, tools remain accessible to users even if the tool's schema changes after authorization. Org admins do not need to re-authorize each tool when its schema is updated by the developer. However, an indication is shown that the tool signature has drifted from what was originally approved.
4. **Review individual tool details:** Admins can review the details of each tool, including its input schema, output schema, and annotations. This helps admins understand what data the tool accepts, what response it returns, and any additional metadata associated with the tool.
5. **Review and reauthorize schema changes:** After an admin authorizes a server, any subsequent changes to tool schemas will require admin review and re-authorization. The admin must review the updated schema and re-authorize to update the approved baseline. This applies regardless of whether the tool signature change setting allows continued access - re-authorization is always needed to formally approve the new schema.

![Agentic App Review Page](<https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltca121c6dcfa6eb84/698aec65885c51f35379d6f2/agentic-app-governance-guide-6.png>)
<br>

Similar functionalities are available in the Resources and Prompts pages.

## Deprecation Labels in Control Hub

Control Hub supports end-to-end lifecycle management for MCP tools, resources, and prompts. **Deprecated** and **Retired** labels help administrators identify affected capabilities. Where available, Control Hub also displays retirement dates, replacement capabilities, and migration guidance so administrators can plan migrations before a capability is retired.

## Refreshing MCP Server Tools in Control Hub

The backend caches each MCP server's tool list for up to one hour. During this period, requests from Control Hub administrators or SDK clients return the cached list. After the cache expires, the next backend request retrieves the latest tools from the MCP server.
