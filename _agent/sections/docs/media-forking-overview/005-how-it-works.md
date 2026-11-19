---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- How it works
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## How it works

When **Start Media Stream** runs for an answered caller-agent conversation, Webex Contact Center establishes a gRPC connection to the registered partner endpoint. Webex Contact Center acts as the gRPC client, and the partner endpoint acts as the gRPC server.

Use a publicly reachable TLS endpoint. Each media RPC carries a signed JWS in the gRPC `authorization` metadata; validate it before processing audio.

![Webex Contact Center copies caller and agent audio over TLS to an external gRPC receiver that validates the JWS and can run custom processing or optional WAV recording.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5ce44070d2255496/6aee2168d18c220b0f50eacd/media-forking-overview.jpg)

1. After the agent answers, Flow Designer runs **Start Media Stream** with the authorized Service App selected as the media destination. For an inbound flow, connect it to the **AgentAccepted** event handler.
2. Webex Contact Center opens a bidirectional gRPC stream to the registered partner endpoint. Caller and agent media can arrive on separate RPCs.
3. The client sends conversation audio in `ConversationAudioForkingRequest` messages.
4. The receiver sample waits for the client to half-close the request stream and finishes processing queued audio. It then sends one final `ConversationAudioForkingResponse` per RPC and closes that response stream. The response can contain acknowledgment, status, or error information.

Although the RPC is bidirectional, the response carries processing status; it does not provide a way for the receiver to send voice back into the call.

For queue-specific conditional logic in Flow Designer, see [Enabling media streaming for specific queues](https://help.webex.com/en-us/article/n5jhgdi/Enabling-media-streaming-for-specific-queues) in the Webex Help Center.
