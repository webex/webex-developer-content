---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Stream virtual-agent audio
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Stream virtual-agent audio

Choose one response mode at the start of the call and keep it for the conversation:

| Mode | Use when | Required completion |
| --- | --- | --- |
| Whole WAV | The complete prompt is already available. | Send one `FINAL` response containing audio with its WAV header, then complete the RPC. |
| Chunked audio | Audio becomes available progressively, such as output from a generative or speech-to-speech model. | Send headerless audio in one or more `CHUNK` responses, then an empty-audio `FINAL`, and complete the RPC. |

For chunked responses, the reference contract allows 100 bytes through 64 KB per chunk. Send chunks as they become available without adding artificial silence; Webex buffers and paces the audio for caller playback.

Each prompt also sets `is_barge_in_enabled`:

- When enabled, caller speech or DTMF can interrupt playback. Webex drops prompts that have not played, and a new input RPC carries the caller input. Stop producing obsolete audio for the interrupted reply when your virtual-agent runtime supports cancellation.
- When disabled, Webex finishes the prompt and caller input received during playback can be dropped.

`disable_prompt_cancellation` controls whether a later partner response can cancel an earlier partial response. It does not disable caller barge-in.
