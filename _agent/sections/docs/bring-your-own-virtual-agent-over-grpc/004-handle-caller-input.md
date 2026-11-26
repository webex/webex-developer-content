---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Handle caller input
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Handle caller input

Each `VoiceVARequest` contains exactly one of these inputs:

| Input | Connector behavior |
| --- | --- |
| `audio_input` | Consume the caller audio stream, detect speech and silence, and send `START_OF_INPUT` and `END_OF_INPUT` at the correct boundaries. |
| `dtmf_input` | Process the ordered DTMF digits and return the next prompt, transfer, or session event. |
| `event_input` | Handle lifecycle events such as `SESSION_START`, `SESSION_END`, `NO_INPUT`, `START_OF_DTMF`, and `CUSTOM_EVENT`. |

The reference connectors process G.711 mu-law caller audio at 8 kHz. Read the encoding and sample rate from each request instead of assuming that all future inputs use the sample defaults.

Send `END_OF_INPUT` only after detecting the end of the caller's utterance. It tells Webex to stop streaming caller audio for that interaction.
