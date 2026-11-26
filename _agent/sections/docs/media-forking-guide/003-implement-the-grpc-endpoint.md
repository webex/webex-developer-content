---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Implement the gRPC endpoint
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Implement the gRPC endpoint

Webex Contact Center acts as the gRPC client. Your partner-hosted service acts as the server and implements this bidirectional streaming RPC:

```protobuf
service ConversationAudio {
  rpc StreamConversationAudio(stream ConversationAudioForkingRequest)
      returns (stream ConversationAudioForkingResponse);
}
```

Handle opening metadata and audio packets separately:

1. Validate the opening message's `conversation_id`, `customer_org_id`, `audio.role`, and `audio.role_id`, and retain the declared encoding and sample rate for that leg. Webex can send this metadata before any audio bytes arrive.
2. Process non-empty `audio.audio_data` as raw audio. Later packets can omit `customer_org_id`, encoding, and sample rate; use only the previously validated metadata for the same conversation and leg. Reject explicit identity mismatches. Preserve `audio.audio_timestamp` when present; do not invent a capture timestamp when it is omitted.
3. Read `audio.role` and `audio.role_id` to identify the media leg.
4. Use `(customer_org_id, conversation_id, role, role_id)` as the processing key so that individual media legs remain separate.
5. Treat re-established streams as separate RPCs. Design downstream idempotency for your consumer; conversation and leg identifiers group media but are not unique packet identifiers. Capture timestamps are not a documented packet sequence.
6. Use `ConversationAudioForkingResponse.status_message` and `error_code` for application status and processing errors. Terminate the RPC with an appropriate gRPC status for authentication, transport, or unrecoverable stream failures.
7. Complete the response stream after Webex completes its request stream and your endpoint finishes processing.

![Caller and agent media use independent RPCs to the same receiver. Each validates its JWS, processes audio, drains queued work after client half-close, and returns one final SUCCESS.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6665993063c98692/6aee373f421b33e40acc9531/media-stream-lifecycle-dual-rpc.jpg)

*Example caller and agent RPCs to the same receiver. Timing is illustrative; each RPC completes independently and can share a TLS connection.*

Caller and agent media can arrive on separate RPCs. Media Forking sends variable-sized raw mono audio frames, not a WAV container, at 8 kHz or 16 kHz. The protobuf defines `LINEAR16`, `MULAW`, and `ALAW`. The canonical Java sample logs the encoding and can append raw audio bytes to files; it does not decode or transcode them. Decode or transcode the audio as required by your downstream processor. The samples send one final `SUCCESS` acknowledgment per RPC after Webex completes its request stream, so do not expect a response for every audio frame.

Implement `Check` on the separate `com.cisco.wcc.ccai.v1.Health` service defined in the sample's [health contract](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/blob/main/media-forking/simulators/media-forking-java/src/main/proto/com/cisco/wcc/ccai/v1/health.proto). Call the gRPC `Check` method on the service endpoint. This contract does not define an HTTP GET health page at `/v1/ping`. Return `SERVING` while the media service is ready to receive streams and `NOT_SERVING` when it is not ready.

> **Important:** The customer is responsible for keeping the receiving service healthy and able to receive and process streamed data. Webex Contact Center does not maintain back pressure. Keep the gRPC receive callback non-blocking; buffer briefly within fixed bounds or shed load explicitly. If the receiver cannot receive or process the stream, any resulting data loss is permanent and cannot be recovered.
