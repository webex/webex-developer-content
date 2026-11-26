---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Choose a webhook family
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks). [Full Markdown](../../../../docs/webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use webhooks to connect Webex activity to your application's workflows, from responding to messages to processing Contact Center events.

## Selected section

## Choose a webhook family

| You need notifications about | Registration and next step |
| --- | --- |
| Messaging, Meetings, Calling, or platform events, including Service App authorization | [Webex Webhooks API: register and manage webhooks](https://developer.webex.com/docs/register-and-manage-webhooks). Use its [receiver guide](https://developer.webex.com/docs/receive-and-verify-webhooks) and [event reference](https://developer.webex.com/docs/webhook-event-reference). |
| Contact Center agents, tasks, captures, or flow failures | [Contact Center: register and manage subscriptions](https://developer.webex.com/docs/using-webhooks). Use its [receiver guide](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks) and [event reference](https://developer.webex.com/docs/webhooks-cc). |
| Device status and events exposed through Workspace Integrations | [Workspace Integration notifications](https://developer.webex.com/docs/workspace-integration-technical-details#webhooks). Configure these notifications through the integration's activation and management flow. |
| Webex Connect messaging and delivery events | [Webex Connect outbound webhooks](https://help.webexconnect.io/docs/outbound-webhooks). |

An application can use more than one family. For example, a Contact Center application can receive platform `serviceApp` authorization events through the Webhooks API and agent events through Contact Center Subscriptions.
