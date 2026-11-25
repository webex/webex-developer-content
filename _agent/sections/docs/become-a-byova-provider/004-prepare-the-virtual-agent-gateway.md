---
type: Excerpt
canonical_url: https://developer.webex.com/docs/become-a-byova-provider
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prepare the virtual-agent gateway
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/become-a-byova-provider). [Full Markdown](../../../../docs/become-a-byova-provider.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Build and operate a Webex App Hub Service App that securely connects your virtual agent gateway to each customer's Webex Contact Center organization.

## Selected section

## Prepare the virtual-agent gateway

Service App authorization and datasource registration let Webex Contact Center
reach your service; they do not prove that the service can handle a customer
conversation. Complete the applicable protocol implementation before asking a
customer to configure a feature or flow.

For a gRPC provider, Webex Contact Center is the gRPC client and your gateway
is the gRPC server. Implement `ProcessCallerInput` for the conversation stream
and `ListVirtualAgents` for agent discovery. Return the real, customer-eligible
agent catalog rather than an empty default response. Also implement the gRPC
health service used by Cisco ping tests and return `SERVING` or `NOT_SERVING`.
See [BYOVA over gRPC](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc) for the
protocol, JWS/JWT validation, and end-to-end gateway checks. For a WebSocket
implementation, use [BYOVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket).
For optional transport-layer client authentication on a gRPC endpoint, see
[mTLS authentication](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication);
it does not replace JWS/JWT validation.
