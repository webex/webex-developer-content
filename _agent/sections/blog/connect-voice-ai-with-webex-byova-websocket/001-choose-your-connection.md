---
type: Excerpt
canonical_url: https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Choose your connection
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket). [Full Markdown](../../../../blog/connect-voice-ai-with-webex-byova-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex Contact Center now supports WebSocket for Bring Your Own Virtual Agent (BYOVA), alongside the existing gRPC interface.

If your voice AI already supports WebSocket, you can now use that protocol to connect it to Webex Contact Center through BYOVA. You can choose the interface that fits your voice AI and development stack.

## Selected section

## Choose your connection

Both interfaces support caller audio, virtual-agent responses, DTMF, conversation events, and transfer to a human agent. They differ in message format and how they carry each interaction.

| Aspect | BYOVA over gRPC | BYOVA over WebSocket |
|---|---|---|
| Message format | Protobuf messages | JSON text messages, with audio encoded as Base64 |
| Interaction lifecycle | A new bidirectional `ProcessCallerInput` RPC for each logical interaction | One connection carries multiple turns throughout the conversation |
| Development approach | Protobuf definitions and generated code | WebSocket libraries and schema-defined JSON messages |

Your connector still adapts your voice AI to the Webex requirements for audio, conversation events, turn completion, interruptions, and handoff. See the [gRPC guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc) and [WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket) for each contract.
