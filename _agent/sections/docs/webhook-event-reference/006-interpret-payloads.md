---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webhook-event-reference
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Interpret payloads
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webhook-event-reference). [Full Markdown](../../../../docs/webhook-event-reference.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Find Webex Webhooks API resources, events, triggers, filters, and links to product-specific payload definitions.

## Selected section

## Interpret payloads

The [common envelope](https://developer.webex.com/docs/receive-and-verify-webhooks#handling-requests-from-webex) identifies the registration, resource, and event. Interpret `data` using the matching resource API. Message notifications can omit sensitive content; retrieve it with an authorized resource request. For `applications`, `data` is a lifecycle snapshot containing `id`, `type`, `name`, `friendlyId`, `orgId`, `createdBy`, and `created`, plus `scopes` when nonempty. An `updated` notification supplies this snapshot rather than a field-level diff. Do not assume it contains every field returned by an application details API.

For field-level schemas, distinguish required, optional, and nullable values using the owning API reference. Preserve field names, casing, and timestamp units. The source catalog does not document those details uniformly, so do not infer them from one example.
