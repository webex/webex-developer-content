---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- What are webhooks?
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks). [Full Markdown](../../../../docs/webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Use webhooks to connect Webex activity to your application's workflows, from responding to messages to processing Contact Center events.

## Selected section

## What are webhooks?

A webhook is an HTTP notification sent to your application when an event occurs. You register the events you want to receive and an HTTPS endpoint in your application. When a matching event occurs, Webex sends a request to that endpoint with a JSON payload describing the event.

Webhooks reduce the need to repeatedly check an API for changes. They work alongside Webex APIs: a notification can start a workflow, and your application can call an API to retrieve more details or take the next action. For example, a message notification identifies the message; your application can then fetch its content with an authorized API request.
