---
type: Excerpt
canonical_url: https://developer.webex.com/docs/provisioning-on-control-hub
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/provisioning-on-control-hub). [Full Markdown](../../../../docs/provisioning-on-control-hub.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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
