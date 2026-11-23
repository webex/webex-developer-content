---
type: Excerpt
canonical_url: https://developer.webex.com/docs/onboard-your-agent
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Step-by-Step Registration Process
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/onboard-your-agent). [Full Markdown](../../../../docs/onboard-your-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

This guide helps developers register an A2A (Agent2Agent) Agentic App on the [Webex Developer Portal](https://developer.webex.com/my-apps/new).

A2A is an open communication standard that enables multiple agents — potentially using different LLMs, runtimes, or toolsets — to exchange messages, delegate tasks, and collaborate. Unlike MCP, which connects one agent to external capabilities, A2A connects multiple agents to each other.

> **Beta**: A2A registration is currently available only in beta. You must sign up for the [beta program](https://developer.webex.com/mcp/docs/webex-developer-beta-program) to access this feature.

## Selected section

## Step-by-Step Registration Process

### 1. Navigate to the Webex Developer Portal

Open <https://developer.webex.com> in your browser.

### 2. Click Start Building Apps

On the home page, click **Start Building Apps** to access the app creation interface.

![Developer Portal landing page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt12f5497065b70803/69c3c91563da6d47145a1e5a/agentic-app-onboarding-guide-1.png)

Alternatively, you can click on your profile, select **My Webex Apps** from the dropdown and click on **Create a New App** on the **My Apps** page that appears.

### 3. Select Create an Agentic App

From the Create a New App page, click **Create an Agentic App** to begin the agentic app registration.

![Create Agentic App option in the app overview page](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc2125de8140f6554/69c3c915d4ca0e2d97b00928/agentic-app-onboarding-guide-4.png)

### 4. Select A2A Module and Enter Server URL

1. **Module**: Select `A2A`.
2. **App URL**: Enter the base HTTPS URL of your A2A server (e.g., `https://agent.example.com`).

![A2A module selection and server URL fields](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1ccef55b32c7ab2d/6a0c37bd94c79e1714263da1/onboard-your-a2a-agentic-app-1.jpg)

### 5. Validate Your Server

Click the **Validate** button. The portal fetches your Agent Card from `{url}/.well-known/agent-card.json` and verifies that:

- The Agent Card has at least one supported interface with `protocolVersion` 1.x.
- At least one supported security scheme is present.

On successful validation, the following fields are auto-populated:

![Validated A2A server details populated from the Agent Card](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf1426bb2722c84b/6a0c37bd07fd976f4f75a147/onboard-your-a2a-agentic-app-2.jpg)

- **Transport Type** — read-only table showing protocol binding, version, and URL from `supportedInterfaces`.
- **Auth Type** — read-only, derived from the Agent Card's `securitySchemes` (e.g., `OAuth 2.0 Authorization Code`, `OAuth 2.0 Client Credentials`, `API Key`).
- **Name** — pre-populated from the Agent Card (editable).
- **Description** — pre-populated from the Agent Card (editable).

### 6. Complete Remaining Fields

- **Name**: Review the pre-populated name or enter a unique name for your app. The name must be unique across all registered agentic apps.
- **Description**: Review or update the description.
- **Logo**: Upload a 512x512 PNG/JPEG or select from the default options.

### 7. Click Add Agentic App

After completing all fields, click the **Add Agentic App** button. The system registers your app and redirects you to the details page.
