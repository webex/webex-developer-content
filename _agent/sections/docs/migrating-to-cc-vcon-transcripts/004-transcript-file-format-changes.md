---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Transcript file format changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

## Transcript file format changes

### Legacy format

```json
{
  "interactionId": "0d9ab80d-6b2a-4170-a3ea-3791c904d604",
  "languageCode": "en-US",
  "responseContents": [
    {
      "recognitionResult": {
        "role": "CALLER",
        "language_code": "en-US",
        "alternatives": [
          {
            "transcript": "Hello, how are you?",
            "confidence": 0.8216304,
            "words": [
              {
                "start_time": {
                  "seconds": 15,
                  "nanos": 329000000
                },
                "end_time": {
                  "seconds": 15,
                  "nanos": 369000000
                },
                "word": "Hello"
              }
            ]
          }
        ]
      }
    }
  ]
}
```

### Voice vCon format

The Voice vCon transcript format follows the vCon structure for conversation data. The example below shows the fields consumers commonly use during migration.

```json
{
  "vcon": "0.4.0",
  "uuid": "bb680ea7-7845-4384-8225-76f2b6270075",
  "language": "en-US",
  "extensions": ["segment_id"],
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
      "start": "2026-04-28T11:59:37.459Z",
      "parties": [0, 1],
      "originator": 0,
      "body": "Hello, how are you?",
      "session_id": {
        "local": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
      },
      "segment_id": "a3b58c75-3f8d-4c8f-a6b2-b05aebe87b13"
    }
  ]
}
```

The Captures API schema label `vcon-04` corresponds to `"vcon": "0.4.0"` in the downloaded JSON. `dialog[].session_id` is an object: read the identifier from `session_id.local`. Its `remote` field may be absent or null when unavailable. `segment_id` may still be included for compatibility; use it as a fallback when `session_id.local` is unavailable.
