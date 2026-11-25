---
type: Excerpt
canonical_url: https://developer.webex.com/docs/choose-your-app-hub-app-type
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Compare app types
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/choose-your-app-hub-app-type). [Full Markdown](../../../../docs/choose-your-app-hub-app-type.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Match listing and authorization to your app](003-match-listing-and-authorization-to-your-app.md)

## Article introduction

Choose the Webex app type that fits your customer workflow, then follow its development and App Hub submission guidance.

## Selected section

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
