---
type: Excerpt
canonical_url: https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Start with Java or Python
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket). [Full Markdown](../../../../blog/connect-voice-ai-with-webex-byova-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Contact Center now supports WebSocket for Bring Your Own Virtual Agent (BYOVA), alongside the existing gRPC interface.

If your voice AI already supports WebSocket, you can now use that protocol to connect it to Webex Contact Center through BYOVA. You can choose the interface that fits your voice AI and development stack.

## Selected section

## Start with Java or Python

Sample code is available in both languages:

- [Java WebSocket sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java): A Spring Boot implementation covering conversation and virtual-agent discovery endpoints, audio and event handling, and handshake authentication.
- [Python BYOVA gateway](https://github.com/webex/webex-byova-gateway-python): A gateway supporting gRPC and WebSocket, with connectors for external voice-agent services. Follow its [WebSocket setup guide](https://github.com/webex/webex-byova-gateway-python/blob/main/docs/WEBSOCKET_TRANSPORT.md) to configure the interface.

These are samples for building and evaluating an integration. You or your implementation partner own the adaptation, hosting, security, capacity, and operations of your deployment.
