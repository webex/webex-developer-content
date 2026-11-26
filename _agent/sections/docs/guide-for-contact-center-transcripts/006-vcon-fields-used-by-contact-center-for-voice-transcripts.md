---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- vCon Fields Used by Contact Center for Voice transcripts
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guide-for-contact-center-transcripts). [Full Markdown](../../../../docs/guide-for-contact-center-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Known Limitations](007-known-limitations.md)

## Article introduction

This guide explains how to find and parse Voice vCon transcript JSON returned through the Captures API. It focuses on the transcript file format; use the [Captures API reference](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) for endpoint details, authorization, request fields, limits, and the full response schema.

---

Voice vCon transcripts may contain conversations between:

- an AI Agent and a user
- a Human Agent and a user
- multiple AI Agents, Human Agents, and a user

The transcript file uses the `vcon` schema, which is based on the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04). In this format, participants are represented in the top-level `parties` array and transcript messages are represented in the top-level `dialog` array.

## Selected section

## vCon Fields Used by Contact Center for Voice transcripts

Voice vCon transcripts follow the vCon structure for conversation data. This guide describes only the voice transcript conventions needed to consume transcript captures. For the complete schema, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

Contact Center consumers commonly use:

- `uuid` as the unique transcript conversation identifier. It equals `data[].taskId` in the Captures API response and identifies the Contact Center interaction.
- `created_at` as the transcript creation timestamp.
- `language` as the transcript language metadata.
- `parties[]` to identify the customer, AI Agent, and Human Agent participants.
- `dialog[]` to read transcript messages.
- `dialog[].originator` to resolve the speaker by index into `parties[]`.
- `dialog[].body` to read the transcript text.
- `dialog[].start` to read the message start timestamp.
- `dialog[].session_id.local` to read the session identifier; `segment_id` may also be present as a compatibility extension.

The `analysis` and `attachments` arrays are part of the vCon object model and may be empty in transcript captures.
