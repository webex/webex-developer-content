---
type: Excerpt
canonical_url: https://developer.webex.com/docs/provisioning-on-control-hub
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Capabilities Configuration
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
