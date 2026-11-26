---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Conversation and RPC lifecycle
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Conversation and RPC lifecycle

The `conversation_id` remains the same for the entire virtual-agent leg, but the gRPC stream does not. Webex opens a new `ProcessCallerInput` bidirectional RPC for each logical interaction, such as session start, caller audio, or DTMF input.

A typical conversation follows this sequence:

1. Webex starts an RPC and sends a `VoiceVARequest` containing the `SESSION_START` event. The first request does not contain synthetic audio.
2. Your connector starts the corresponding session with its virtual agent and returns the welcome prompt.
3. Webex finishes sending requests for that RPC and half-closes its side of the stream.
4. After sending every response for that interaction, your connector completes its side of the RPC.
5. Webex opens another RPC for the next caller input while reusing the same `conversation_id`.
6. When the caller hangs up, Webex sends `SESSION_END`. A connector can instead return `TRANSFER_TO_AGENT`, `SESSION_END`, or a configured `CUSTOM_EVENT` to leave the virtual-agent flow.

Complete every RPC normally after its responses are sent. Use gRPC error status only for unexpected failures; do not leave a completed interaction open while waiting for the next turn.
