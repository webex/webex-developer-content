---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authentication and network requirements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Authentication and network requirements

The production WebSocket endpoint must meet these requirements:

- Expose a publicly reachable `wss://` URL on a partner-owned domain registered in the Service App's **Data Exchange Domain**.
- Use TCP port 443 unless Webex has approved a different port for the environment.
- Present a valid TLS server certificate whose identity matches the registered hostname and whose trust chain is accepted by Webex.
- Accept a standard WebSocket upgrade and long-lived bidirectional JSON text-frame connection.
- Accept the `Authorization: Bearer <token>` header sent by Webex and validate the token according to the BYODS authentication contract.
- Configure firewalls, web application firewalls, reverse proxies, and load balancers so that they do not block WebSocket upgrades, application `PING` and `PONG`, expected message sizes, or long-lived connections.
- Scale for one concurrent WebSocket connection per active virtual-agent conversation.

Private, loopback, link-local, and plaintext `ws://` endpoints are not valid production partner targets. Do not place credentials in the URL.

Mutual TLS (mTLS) is not required for BYOVA over WebSocket. The current WebSocket contract uses server-authenticated TLS plus bearer-token validation. Optional BYOVA mTLS applies to the gRPC variant, not this WebSocket contract, and does not replace application token validation.

The AsyncAPI specification does not publish stable Webex source IP ranges. If the partner requires source-IP allowlisting, obtain the supported environment- and region-specific egress requirements from Webex support instead of allowlisting IP addresses observed during testing.
