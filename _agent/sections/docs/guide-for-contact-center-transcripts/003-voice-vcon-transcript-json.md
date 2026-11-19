---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Voice vCon Transcript JSON
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

## Voice vCon Transcript JSON

The downloaded Voice vCon transcript file is a vCon-style JSON object with conversation metadata, participants, and dialog entries. For the full standard object model, see the [vCon JSON object definition](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-3).

```json
{
  "vcon": "0.4.0",
  "uuid": "bb680ea7-7845-4384-8225-76f2b6270075",
  "created_at": "2026-04-28T11:59:26.617Z",
  "extensions": [
    "segment_id"
  ],
  "language": "en-US",
  "parties": [
    {
      "role": "customer"
    },
    {
      "uuid": "69e23483c39ab81f25fa9bc8",
      "role": "virtual-agent"
    }
  ],
  "dialog": [
    {
      "start": "2026-04-28T11:59:26.623Z",
      "type": "text",
      "parties": [
        0,
        1
      ],
      "originator": 1,
      "mediatype": "text/plain",
      "encoding": "utf-8",
      "body": "Welcome to Sapna Book House! Hi there, How can I help you today?",
      "session_id": {
        "local": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
      },
      "segment_id": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
    },
    {
      "start": "2026-04-28T11:59:37.459Z",
      "type": "text",
      "parties": [
        0,
        1
      ],
      "originator": 0,
      "mediatype": "text/plain",
      "encoding": "utf-8",
      "body": "Hello, how are you?",
      "session_id": {
        "local": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
      },
      "segment_id": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
    }
  ],
  "analysis": [],
  "attachments": []
}
```

The object above is referred to as the Voice vCon transcript JSON in the rest of this guide.
