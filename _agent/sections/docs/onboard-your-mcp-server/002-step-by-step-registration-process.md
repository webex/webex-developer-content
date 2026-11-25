---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-mcp-server
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Step-by-Step Registration Process
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/onboard-your-mcp-server). [Full Markdown](../../../../docs/onboard-your-mcp-server.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This guide helps developers register their MCP server on the [Webex Developer Portal](https://developer.webex.com/my-apps/new). For A2A (Agent2Agent) Agentic Apps, see [Onboard Your Agent](https://developer.webex.com/docs/onboard-your-agent).

## Selected section

## Step-by-Step Registration Process

### 1. Navigate to the Webex Developer Portal

Open <https://developer.webex.com> in your browser.


### 2. Click Start Building Apps

On the home page, click **Start Building Apps** to access the app creation interface.

![Developer Portal landing page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt12f5497065b70803/69c3c91563da6d47145a1e5a/agentic-app-onboarding-guide-1.png)

Alternatively, you can click on your profile, select **My Webex Apps** from the dropdown and click on **Create a New App** on the **My Apps** page that appears (you will directly be taken to the app creation interface if you don't have any pre-existing apps).

![My Webex Apps dropdown](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf7b89cf2e3655ad/69c3c915d4ca0e3747b00924/agentic-app-onboarding-guide-2.png)

![Create a New App button](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt864b552d82a2bc35/69c3c914191b6b4e3c7c8194/agentic-app-onboarding-guide-3.png)

### 3. Select Create an Agentic App

From the Create a New App page, click **Create an Agentic App** to begin the agentic app registration.

![Create Agentic App option in the app overview page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc2125de8140f6554/69c3c915d4ca0e2d97b00928/agentic-app-onboarding-guide-4.png)

### 4. Enter App Details

Fill in the following fields:

- **Module**: Select `MCP` (A2A coming soon).
- **Transport Type**: Select `Streamable HTTP` or `HTTP SSE`.
- **Name**: Unique name for your app.
- **Description**: Clear description of its purpose.
- **Logo**: Upload a 512x512 PNG/JPEG (or select from 3 default options).
- **App URL**: Public HTTPS endpoint.
- **Authentication types**: Select one or more methods available for your MCP server:
  - **OAuth 2.0 client credentials**
  - **OAuth 2.0 authorization code**
  - **API key**
  - **User token**
  - **Custom headers**
  - **Webex Service App** (eligible Webex-hosted MCP servers only)

#### Webex Service App authentication

For an eligible Webex-hosted MCP server, select **Webex Service App** to use an organization-level machine identity. The option appears only after you enter an eligible MCP server URL.

You don't enter a client ID, client secret, or access token. The app details page displays the **Associated Webex Service App ID** after provisioning succeeds.

Each customer organization authorizes the Service App separately. In Control Hub, a Full Administrator opens **Apps > Agentic Apps**, selects the MCP server, and opens the **Authentication** tab. The administrator selects **Webex Service App** as the active authentication method and uses the **Service Apps page** link to review the associated app and its requested scopes. See [Webex Service App authentication in Control Hub](https://developer.webex.com/docs/provisioning-on-control-hub#webex-service-app) for this flow and [Full Admin Authorization of a Service App](https://developer.webex.com/docs/service-apps#full-admin-authorization-of-a-service-app) for the separate authorization step. If the requested scopes change later, a Full Administrator must review and reauthorize the updated scopes.

![Agentic App registration form](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7a2850498ca94d5d/69c3c9155930181788eb2e87/agentic-app-onboarding-guide-5.png)

![Agentic App registration form continued](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbf4dc97560c58e5c/69c3c915593018772beb2e83/agentic-app-onboarding-guide-6.png)

### 5. Click Add Agentic App

After completing all fields, click on the **Add Agentic App** button at the bottom of the registration page. The system will register your app and redirect you to the details page.

The details page can also be accessed by going to the **My Apps** page and selecting the app you registered.

![Agentic App details page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8707435361f4454c/69c3c9145dd8290da7c30856/agentic-app-onboarding-guide-7.png)
