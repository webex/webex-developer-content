---
type: Article
title: Introducing Group-Level Access for Webex MCP Servers
canonical_url: https://developer.webex.com/blog/introducing-group-level-access-for-webex-mcp-servers
content_type: blog
date: '2026-10-13'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-group-level-access-for-webex-mcp-servers)

Administrators can now configure group-level access for Webex MCP servers connected to external AI agents and clients, such as Claude Desktop, Cursor, and VS Code. In Webex Control Hub, **Limited access** lets you choose which groups discover a server's enabled functions, with one shared audience for all functions or different groups for individual tools, resources, and prompts.

For connection setup and authentication, follow [Connect Webex MCP Servers to External Clients](https://developer.webex.com/mcp/docs/webex-agentic-mcp-servers).

Different teams need different capabilities. A support team might need to discover functions from the Webex Contact Center MCP server in its AI client, while a pilot group evaluates a new connection. Group-level access lets administrators introduce those capabilities to a smaller audience and expand the audience as the rollout progresses.

### Start with a shared audience

Choose **Same groups for all functions** when the same team should discover every enabled function in a server. For example, you could select **Support Team** and **Pilot Users** for an initial rollout.

1. Sign in to [Webex Control Hub](https://admin.webex.com/) and go to **Apps > Agentic Apps**.
2. Select the MCP server and open **General**.
3. Under **Access**, select **Limited access**, then **Same groups for all functions**.
4. Open **Search groups**, select the groups, and select **Save**.

![Control Hub Limited access with Support Team and Pilot Users selected for all functions.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt82fb37ddc87ef26e/6ace4078ea4b09acc937585d/agentic-limited-access-same-groups.jpg)

The groups must already exist in your organization. You can create them under **Management > Groups** in Control Hub. Keep their membership current as people join or leave the rollout.

### Give individual functions different audiences

Choose **Different groups per function** when functions need separate audiences. You might assign a lookup function to a support team and a configuration function to a smaller pilot group. Each function has its own group selection.

On the server's **General** tab, select **Limited access**, choose **Different groups per function**, and select **Save**.

![Control Hub Limited access with Different groups per function selected.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6484e0c1a6614c32/6ace40b02961026746bdc562/agentic-limited-access-per-function.jpg)

Open **Tools**, **Resources**, or **Prompts**. Find the function you want to configure and select **Edit** in its **Group access** column. The Tools tab below shows where to configure **List Flows**.

![Control Hub Tools table with an Edit control in the Group access column for each function.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltee73d7cf12eba081/6ace4e3cd2452a39eba44934/agentic-per-function-tools-group-access.jpg)

On **Edit group access**, select the groups in **Search groups**, then select **Save**. Repeat for each enabled function you want users to discover. The example below shows **Support Team** selected for **List Flows**; **Pilot Users** is another available group.

![Edit group access for List Flows with Support Team selected and Pilot Users available in Search groups.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta345b5b22115005a/6ace4e7ddbf6ce411c0242e4/agentic-per-function-list-flows-group-picker.jpg)

In this mode, a user must belong to at least one group assigned to a function to discover it. An enabled function with no assigned groups has no matching users. Saving an empty selection removes the function from group-based discovery.

### Check the rollout

After saving, reopen **General** to confirm the access mode. For per-function assignments, return to the function's **Edit** screen on **Tools**, **Resources**, or **Prompts** and check its saved groups.

Group assignment controls discovery of enabled functions. It does not enable a disabled function, and the MCP server's own authentication and authorization controls still apply when a function is invoked.

MCP actions in [Webex AI Agent Studio](https://developer.webex.com/docs/mcp-ai-agent-studio) continue to use organization-level access. Group-level access is not supported for those actions.

Follow the [Provisioning on Control Hub guide](https://developer.webex.com/create/docs/provisioning-on-control-hub#group-level-access) for the full configuration steps, authentication options, and capability settings. Use the [Admin Approval Guide for Agentic Apps](https://developer.webex.com/mcp/docs/admin-approval-guide-for-agentic-apps) to review the server before enabling it for your organization.
