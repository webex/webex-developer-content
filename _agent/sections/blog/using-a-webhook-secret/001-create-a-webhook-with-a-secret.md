---
type: Excerpt
canonical_url: https://developer.webex.com/blog/using-a-webhook-secret
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Create a webhook with a secret
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/using-a-webhook-secret). [Full Markdown](../../../../blog/using-a-webhook-secret.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

> **Info**
>
> Updated September 2026: This post has been refreshed with current Webex webhook security guidance.



Webhooks send HTTP POST requests to the public URL you provide. A shared secret lets your receiver verify the request before it parses or processes the payload.

## Selected section

## Create a webhook with a secret

Add a `secret` when you [create a webhook](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook). For example:

```json
{
  "name": "New message in a project room",
  "targetUrl": "https://example.com/webex-events",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=YOUR_ROOM_ID",
  "secret": "replace-with-a-strong-random-secret"
}
```

Store the secret in your server's secret manager or environment configuration. Do not put it in source control, a client application, or a log.
