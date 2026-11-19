---
type: Excerpt
canonical_url: https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Enablement Scope & Assignment
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps). [Full Markdown](../../../../docs/admin-approval-guide-for-agentic-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

This is a review guide for organization administrators evaluating and approving MCP Servers and A2A Agents before enabling them for organizational users. It provides guidelines to validate that an agentic app meets security, quality, and governance standards.

---

## Selected section

## Enablement Scope & Assignment

When you approve an MCP server, you also decide **who in your org may use it** and **at what granularity**. The **General** tab in Control Hub uses the following labels:

| Dimension | Choices |
|-----------|---------|
| Audience | **Allowed for all users** or **Limited access** |
| Assignment mode under **Limited access** | **Same groups for all functions** or **Different groups per function** |

Use **Blocked for all users** when the server should not be available to your organization. Follow [Provisioning on Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub#group-level-access) for configuration steps. Group-level access does not apply to MCP actions in Webex AI Agent Studio; those actions use organization-level access.

### Org vs. Group Enablement

| Choice | When to Use | Trade-off |
|--------|------------|-----------|
| **Allowed for all users** | Low-risk, broadly useful tools (e.g., calendar lookups, generic search) | Makes enabled functions discoverable to all users in your organization |
| **Limited access** | Functions intended for selected groups, such as role-specific workflows | Limits enabled-function discovery by group membership; requires current group lists |

With **Limited access**, you choose the groups that should discover the server's enabled functions. Discovery compares the user's groups from your organization's identity with the configured groups. A function appears only when at least one group matches. These settings govern enabled-function discovery; the MCP server's own authentication and authorization controls still apply when a function is invoked.

### Shared vs. Per-Function Assignment

| Choice | Behavior | When to Use |
|--------|---------|------------|
| **Same groups for all functions** | The selected groups apply to all enabled tools, resources, and prompts | Most apps. Simpler to reason about; fewer settings to maintain |
| **Different groups per function** | Each function has its own group selection, configured on **Tools**, **Resources**, or **Prompts** | Apps where some functions need a different audience from others |



> **Best Practice**
>
> Start with **Same groups for all functions**. Choose **Different groups per function** when functions need different audiences. Review each function's group list regularly to keep access aligned with your intent.



---
