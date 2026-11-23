---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Adapt and verify the connector
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Adapt and verify the connector

Before onboarding a customer:

1. Return your real agent catalog from `ListVirtualAgents`.
2. Map audio, DTMF, and input events to your virtual-agent runtime.
3. Stream prompts and output events using the required response finality.
4. Verify `SESSION_START`, multi-turn audio, DTMF, barge-in, transfer, custom event, caller hang-up, and connector error scenarios.
5. Confirm JWT rejection and, when enabled, mTLS rejection before testing valid credentials.
6. Add production monitoring, timeouts, capacity limits, and graceful shutdown behavior around the sample implementation.

The sample connector demonstrates the protocol; the partner remains responsible for hosting, scaling, securing, and supporting the production service.
