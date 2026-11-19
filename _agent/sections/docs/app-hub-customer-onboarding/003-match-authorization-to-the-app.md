---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-customer-onboarding
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Match authorization to the app
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-customer-onboarding). [Full Markdown](../../../../docs/app-hub-customer-onboarding.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Write the customer setup instructions](004-write-the-customer-setup-instructions.md)

## Article introduction

Help customers connect your App Hub app by separating developer preparation from customer authorization, configuration, and verification.

## Selected section

## Match authorization to the app

| App or solution | Customer handoff | Detailed guidance |
| --- | --- | --- |
| OAuth integration | The user signs in and consents to the requested scopes, subject to organization policies. | [Integrations](https://developer.webex.com/docs/integrations) and [Authentication](https://developer.webex.com/docs/authentication) |
| Service App | A customer Full Admin reviews and authorizes the app. The developer then obtains credentials for that authorizing organization. Follow the documented App Hub submission path before requesting authorization in a non-affiliated organization. | [Service Apps](https://developer.webex.com/docs/service-apps) |
| BYOVA solution | The customer authorizes the provider's Service App and configures Contact Center. The provider handles its customer-specific onboarding and datasource connection. | [BYOVA provider guide](https://developer.webex.com/docs/become-a-byova-provider) |
| Embedded app | Explain the supported meetings, spaces, or sidebar context and applicable organization controls. If the app also uses an OAuth integration, explain that separate consent step. | [Embedded Apps developer guide](https://developer.webex.com/docs/embedded-apps-guide) |
| Bot | Explain how to find or add the bot and start its supported interaction. If your solution also uses an integration, document its separate authorization step. | [Bots](https://developer.webex.com/docs/bots) |
| Workspace integration | A customer administrator activates the integration in Control Hub and reviews its device access. | [Workspace Integrations](https://developer.webex.com/docs/workspace-integrations) |
| Agentic app | Provide the server information and usage instructions the customer administrator needs for review and enablement. Check availability and prerequisites for the chosen protocol. | [Admin Approval Guide for Agentic Apps](https://developer.webex.com/docs/admin-approval-guide-for-agentic-apps) |

BYOVA is a solution journey built on a Service App and Contact Center configuration, rather than a separate app registration type. Service App authorization alone does not configure call routing.
