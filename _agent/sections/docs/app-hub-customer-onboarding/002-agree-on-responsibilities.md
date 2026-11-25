---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-hub-customer-onboarding
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Agree on responsibilities
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-hub-customer-onboarding). [Full Markdown](../../../../docs/app-hub-customer-onboarding.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Match authorization to the app](003-match-authorization-to-the-app.md) [Write the customer setup instructions](004-write-the-customer-setup-instructions.md)

## Article introduction

Help customers connect your App Hub app by separating developer preparation from customer authorization, configuration, and verification.

## Selected section

## Agree on responsibilities

| App developer | Customer |
| --- | --- |
| Operate the application and maintain its registration, listing, and support contact. | Identify the users and administrators who will approve and use the app. |
| Explain supported products, required accounts or licenses, requested permissions, and data use. | Confirm product access and review permissions against organization policies. |
| Provide setup instructions and a way to verify the customer connection. | Complete the applicable authorization and product configuration steps. |
| Support failed setup, credential recovery, and offboarding. | Test the intended workflow and follow the removal instructions when access is no longer needed. |

Keep developer-owned client secrets and customer access tokens in your service's approved secrets store. Do not ask customers to send these credentials through email, chat, or a support ticket.
