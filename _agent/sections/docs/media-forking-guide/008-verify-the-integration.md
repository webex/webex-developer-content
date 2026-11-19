---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Verify the integration
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Verify the integration

1. Confirm that the health `Check` RPC reports `SERVING` when the receiver is ready and `NOT_SERVING` when it is not ready.
2. Confirm that the endpoint rejects an audio RPC that does not contain a valid JWS.
3. Place a test call through the configured flow.
4. Have an agent answer the call.
5. Confirm that the **Start Media Stream** activity opens a stream to the registered endpoint.
6. Confirm receipt of non-empty audio for both `CALLER` and `AGENT` roles, including when they use separate RPCs.
7. Verify that the endpoint preserves conversation and role identifiers.
8. Verify that the endpoint handles opening metadata, sparse audio packets, and the declared encoding and sample rate. Record whether capture timestamps are supplied.
9. End the call and confirm that both sides close the stream cleanly.
10. Check server logs for expired tokens, URL or schema claim mismatches, stream failures, and successful completion.
