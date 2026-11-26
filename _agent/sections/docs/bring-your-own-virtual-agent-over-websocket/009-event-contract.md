---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Event contract
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-websocket.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](003-before-you-begin.md) [Authentication and network requirements](011-authentication-and-network-requirements.md)

## Article introduction

Implement a partner-hosted WebSocket virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center over one secure connection per conversation.

## Selected section

## Event contract

Event names are directional. A partner must not send an output-only event as an input event or interpret an input event as a partner output.

| Event or input | Direction | Partner behavior |
| --- | --- | --- |
| `SESSION_START` | Webex to partner | First application input on the connection. Initialize conversation state and optionally send a welcome response. |
| `audio_input` | Webex to partner | Process caller audio using the encoding and sample rate in the request. |
| `dtmf_input` | Webex to partner | Process the ordered DTMF digit list. Supported digits are 0-9, A-D, `*`, and `#`. |
| `START_OF_DTMF` | Webex to partner | Treat as an interruption associated with DTMF input. The schema does not define a separate literal `BARGE_IN` input event. |
| `NO_INPUT` | Both directions | Use direction and surrounding state to distinguish a Webex input notification from a partner recognition outcome. |
| `START_OF_INPUT` | Partner to Webex | Report that the partner detected caller speech. This event supports barge-in and input-boundary handling. |
| `END_OF_INPUT` | Partner to Webex | Report that the partner's endpointing or end-of-turn detector considers caller input complete. |
| `NO_MATCH` | Partner to Webex | Report that caller input was detected but could not be matched or understood. |
| `TRANSFER_TO_AGENT` | Partner to Webex | Request handoff from the virtual-agent leg. Include only metadata agreed for the integration. |
| `CUSTOM_EVENT` | Both directions | Map the event `name` and its parameters or metadata to an agreed partner-specific behavior. |
| `SESSION_END` | Both directions | End the application session and the virtual-agent leg. |

The partner owns speech-start and end-of-turn detection. Send the corresponding output events when the partner's speech or speech-to-speech runtime reaches those boundaries; do not wait for Webex to infer the partner's turn state.

### Barge-in

To allow the caller to interrupt a prompt, set `prompts[].is_barge_in_enabled` to `true`. When the partner detects new caller speech, send `START_OF_INPUT`. Webex uses the prompt setting and input event to stop or flush interruptible playback and continue with the caller turn.

The WebSocket schema does not contain a literal `BARGE_IN` event. Do not wait for a message with that name. DTMF interruption is represented separately through DTMF input and `START_OF_DTMF`.

### DTMF

Webex sends an ordered `dtmf_events` array in `dtmf_input`. Map each enum to the corresponding digit while preserving order. The partner can use `input_mode` and `input_handling_config.dtmf_config` in its response to control whether the next input accepts DTMF, the requested digit count, termination character, and inter-digit timeout.

### Transfer and handoff

To request transfer, send `TRANSFER_TO_AGENT` in `output_events`. The partner owns the decision to transfer and the agreed event metadata. Webex owns ending the virtual-agent leg and executing the Contact Center transfer or handoff configured for the flow.

When transcript publication is enabled, the agent handoff transcript can contain the accumulated caller and virtual-agent conversation from the virtual-agent leg. It is not a partner-generated post-call summary.
