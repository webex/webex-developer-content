---
type: Excerpt
canonical_url: https://developer.webex.com/docs/choose-your-app-hub-app-type
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Match listing and authorization to your app
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/choose-your-app-hub-app-type). [Full Markdown](../../../../docs/choose-your-app-hub-app-type.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Choose the Webex app type that fits your customer workflow, then follow its development and App Hub submission guidance.

## Selected section

## Match listing and authorization to your app

App registration, App Hub publication, and customer authorization are separate steps. Use the requirements for your app type:

- **OAuth integrations:** Register the integration and implement OAuth consent. An App Hub listing provides discovery; it does not replace user consent or override an organization's integration controls.
- **Service Apps:** To request authorization in a non-affiliated organization, follow the App Hub submission and review path described in [Service Apps](https://developer.webex.com/docs/service-apps). Listing alone does not authorize the app for a customer.
- **Bots:** Implement and test the bot's user interaction before submitting. Check the submission rules if the bot also depends on an integration.
- **Embedded apps:** Complete the [Submission Checklist for Embedded Apps](https://developer.webex.com/docs/app-hub-submission-checklist-for-embedded-apps) and the design guidance for each supported context.
- **Workspace integrations:** Follow the public integration onboarding process in [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations). Its Control Hub activation and deployment process has its own requirements.
- **Agentic apps:** Follow [Submit to App Hub & Badging](https://developer.webex.com/docs/agentic-apps-app-hub), then give customers the [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps).
