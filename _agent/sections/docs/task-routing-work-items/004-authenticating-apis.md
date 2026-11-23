---
type: Excerpt
canonical_url: https://developer.webex.com/docs/task-routing-work-items
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Authenticating APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/task-routing-work-items). [Full Markdown](../../../../docs/task-routing-work-items.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before You Begin](003-before-you-begin.md)

## Article introduction

Work Items enable external systems to inject non-conversational tasks into Webex Contact Center and can be orchestrated within Webex CC Flow Designer, routed, handled, monitored, and reported alongside other contact center channel interactions.

**Note:** 
- Work Items do NOT represent live messaging conversations for unsupported channels such as Viber, Instagram, third-party digital channel gateways, etc. A bring-your-own messaging channel should be used for such use cases.
- Use Work Items specifically for backend or offline tasks such as CRM leads, claims, faxes, cases, purchase orders, or other work that needs contact center routing and agent handling without a customer messaging on the other side.

Availability for Work Items is currently open for **BETA**. Contact your Cisco team to request access.

## Selected section

## Authenticating APIs

Work Item injection leverages a [Service App](https://developer.webex.com/docs/service-apps) that will represent your middleware so that access token handling is managed appropriately for server-side operations.

For `scope` definitions, refer to [Integration Scopes](https://developer.webex.com/docs/integration-scopes).

### Create and authorize a service app

1. Sign in to the developer portal and create a new **Service App**
2. Capture the client secret when it is first shown. After the app is submitted for authorization, regenerate the secret if it was not saved.
3. Assign the required scopes:
   - `cjp:task_write`
   - `cjp:task_read`
4. Ask the customer administrator to authorize the Service App in Control Hub under **Apps**.
5. After authorization, return to the Service App in the developer portal, select the authorized organization, provide the client secret, and generate the access token.
6. Use the resulting access token when calling the Create Task API and the Task Messages API.

For this integration pattern, ensure that:

- The Service App is authorized for the customer organization
- The `access_token` includes `cjp:task_write` for Create Task and Task Messages
- The `access_token` includes `cjp:task_read` when task read access is required

### Refreshing access tokens  

If your integration needs long-running access, retain the refresh token and use the standard OAuth refresh flow described in the [Authentication guide](https://developer.webex.com/docs/authentication#using-the-refresh-token) before the current access token expires.

For server-to-server integrations, store the `client_secret`, `access_token`, and `refresh_token` securely, and rotate or regenerate credentials according to your organization's security practices.
