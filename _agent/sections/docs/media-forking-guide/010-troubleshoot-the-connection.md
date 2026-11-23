---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshoot the connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Troubleshoot the connection

| Symptom | Check |
| --- | --- |
| Service App is unavailable or cannot be authorized | Confirm the Media Forking subscription, selected schema, app visibility, and customer admin authorization. A data-source registration alone does not establish entitlement. |
| No configuration appears under Integrations > Features | Select the Service App directly in **Start Media Stream**; the flow does not need a separate Features configuration. |
| `callNotAnswered` | Start streaming after the agent answers, using the agent-answer event handler described above. |
| No connection or unhealthy receiver | Check the registered hostname and URL, publicly trusted TLS certificate, HTTP/2 routing, and Cisco gRPC health `Check`. An HTTP health page does not implement that contract. |
| `UNAUTHENTICATED` | Check signed expiry and the registered issuer, audience, subject, URL, schema, and organization bindings. Renew an expired data-source JWS with a fresh nonce and the complete update payload. Keep token values out of logs. |
| Audio arrives without metadata fields or timestamps | Retain validated opening metadata for that leg and preserve missing timestamps as absent. Do not reject a packet only because inherited fields are omitted. |
| Recording fails or only a `.partial` file exists | Check directory permissions, write/search access, disk space, and stream failure logs. A finalized WAV can still contain only part of a call. |
