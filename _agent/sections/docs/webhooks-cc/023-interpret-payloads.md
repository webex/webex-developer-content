---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhooks-cc
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Interpret payloads
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhooks-cc). [Full Markdown](../../../../docs/webhooks-cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Contact Center webhook event types, resource versions, and event-specific payload fields.

---

<a id="using-webhooks"></a>

<a id="overview"></a>

## Selected section

## Interpret payloads

Every event uses the [common Contact Center webhook envelope](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#anatomy-of-a-webhook). Its `type` is the event identifier shown above, such as `agent:login` or `task:connected`. The field tables describe the contents of `data`.

Field types, optional markers, and examples are event-specific. Preserve field names, casing, and timestamp units. Do not infer a shared payload schema or required fields from another event's example.

See the receiver guide for [signature verification](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#request-verification) and [delivery acknowledgements](https://developer.webex.com/docs/receive-and-verify-contact-center-webhooks#response).
