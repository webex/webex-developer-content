---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Reading Messages
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

## Reading Messages

Each item in `dialog` represents a transcript message or utterance, following the vCon [dialog object](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-4.3) model.

Read message values directly from each `dialog[]` entry:

- `dialog[].body` contains the transcript text.
- `dialog[].start` contains the message timestamp.
- `dialog[].originator` contains the index of the speaker in the top-level `parties[]` array.
- `dialog[].session_id.local` contains the session identifier when present. For AI Agent dialogs, this represents the AI Agent session ID; for recording-derived Human Agent transcripts, it represents the interaction ID.

`session_id` is an object, following the vCon [session identifier model](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-4.3.12). Read its `local` field rather than treating the object as a string. `remote` may be absent or null when unavailable. The `segment_id` extension may still be included for compatibility; use it as a fallback when `session_id.local` is unavailable.

Read transcript entries from `dialog[]`; their order may differ from the Session UI in some flows. Voice vCon transcripts use entry-level timestamps; they do not include word-level timing or confidence scores in the transcript JSON.

```python
parties = transcript.get("parties") or []

for dialog_entry in transcript.get("dialog") or []:
    originator = dialog_entry.get("originator")
    speaker = parties[originator] if isinstance(originator, int) and 0 <= originator < len(parties) else {}

    timestamp = dialog_entry.get("start")
    speaker_role = speaker.get("role")
    speaker_id = speaker.get("uuid")
    message_text = dialog_entry.get("body")
    session_id = dialog_entry.get("session_id")
    session_identifier = (
        session_id.get("local") if isinstance(session_id, dict) else None
    ) or dialog_entry.get("segment_id")

    print(timestamp, speaker_role, speaker_id, message_text, session_identifier)
```
