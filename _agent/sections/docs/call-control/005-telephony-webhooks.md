---
type: Excerpt
canonical_url: https://developer.webex.com/docs/call-control
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Telephony WebHooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/call-control). [Full Markdown](../../../../docs/call-control.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Authentication and Authorization](002-authentication-and-authorization.md)

## Article introduction

Third-party services integrate with Webex Calling using admin-level APIs and admin-level tokens provided via Service Apps. This guide covers authentication, call control APIs, discovery APIs, telephony webhooks, and interest registration.

## Selected section

## Telephony WebHooks

WebHooks are used across Webex to notify your app about events or activities happening on the Webex platform.

The Webex Calling platform exposes webhook resources. These resources are labeled with the `telephony_` prefix.

For more information about Webex Webhooks, see the [Webhooks Guide](https://developer.webex.com/docs/webhooks).

### Org-Level WebHooks

Telephony Webhooks leverage org-level WebHooks. By registering a WebHook with the `ownedBy` field set to `org`, a Service App can receive the events for all actors in an organization. Only org-level WebHooks are supported for Service Apps. Only a subset of telephony webhooks support org-level webhooks and can therefore be used by Service Apps.

### Telephony Resource Definitions

| Resource | Events | Required Scope | Description |
|----------|--------|----------------|-------------|
| `telephony_calls` | created, updated, deleted | `spark-admin:calls_read` | Notification of calls progression through each state |
| `telephony_agent` | updated | `spark-admin:calls_read` | Notification of call queue agent changes |
| `telephony_agentMonitoring` | updated | `spark-admin:calls_read` | Notification of call queue agent performance metrics |
| `telephony_queue` | updated | `spark-admin:calls_read` | Notification of call queue calls progression |
| `telephony_queueMonitoring` | updated | `spark-admin:calls_read` | Notification of call queue performance metrics |

### Webhook Registration Example

```bash
curl -L --request POST \
  --url 'https://webexapis.com/v1/webhooks' \
  --header 'Authorization: Bearer $ACCESS_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
    "name": "My agentMonitoring Webhook",
    "targetUrl": "https://example.com/my-endpoint",
    "resource": "telephony_agentMonitoring",
    "event": "all",
    "ownedBy": "org"
  }'
```

For detailed webhook payload schemas and examples, see <a href="https://developer.webex.com/docs/call-control#webhook-payload-schemas">Webhook Payload Schemas</a> at the end of this guide.

---
