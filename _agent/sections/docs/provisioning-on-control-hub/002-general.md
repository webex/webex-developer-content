---
type: Excerpt
canonical_url: https://developer.webex.com/docs/provisioning-on-control-hub
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- General
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/provisioning-on-control-hub). [Full Markdown](../../../../docs/provisioning-on-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication](003-authentication.md)

## Article introduction

Use the [Webex Control Hub](https://admin.webex.com/) to provision Agentic Apps for your organization. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.

---



> **Info**
>
> Users acknowledge and agree that they bear full responsibility for understanding, complying with, and managing all aspects of the liability framework related to their use of MCP applications.





> **Info**
>
> This guide is for administrators only. This includes configuring user access and authentication, and defining governance controls to manage which agentic capabilities are available to organizational users.

## Selected section

## General

Select an app and open the **General** tab. Under **Access**, choose who can use the app:

- **Blocked for all users**: Block access for your organization.
- **Allowed for all users**: Allow access for your organization.
- **Limited access**: Limit discovery of an MCP server's enabled functions to users in selected groups. You can use the same groups for all functions or assign different groups per function.

Select **Save** to apply your changes. For group configuration, follow [Group-Level Access](https://developer.webex.com/docs/provisioning-on-control-hub#group-level-access).

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

Group access controls the audience; it does not enable a disabled function. Review the function's enablement settings in [Capabilities Configuration](https://developer.webex.com/docs/provisioning-on-control-hub#capabilities-configuration).

For MCP actions in [Webex AI Agent Studio](https://developer.webex.com/docs/mcp-ai-agent-studio), group-level access is not supported; tool access is managed at the organization level.
