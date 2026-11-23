---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Download the Transcript JSON
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

## Download the Transcript JSON

After the Captures API returns metadata, the transcript-specific flow is:

1. Read the `data[].transcription[]` array for the task.
2. Select a transcription entry where `source` is `realtime-voice` or `recording` and `transcriptSchemaVersion` starts with `vcon-`.
3. Make an HTTP `GET` request to that entry's `filePath`.
4. Parse the returned JSON as a Voice vCon transcript, following the [vCon object model](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-3). Current captures labeled `vcon-04` contain `"vcon": "0.4.0"` in the downloaded JSON.

Example:

```python
import requests


def fetch_vcon_transcript(captures_response):
    task = (captures_response.get("data") or [{}])[0]
    transcriptions = task.get("transcription") or []

    transcript_capture = next(
        (
            item
            for item in transcriptions
            if item.get("source") in {"realtime-voice", "recording"}
            and (item.get("transcriptSchemaVersion") or "").startswith("vcon-")
        ),
        None,
    )

    if not transcript_capture or not transcript_capture.get("filePath"):
        raise ValueError("Voice vCon transcript capture not found")

    try:
        response = requests.get(transcript_capture["filePath"], timeout=30)
        response.raise_for_status()
    except requests.RequestException:
        raise RuntimeError("Transcript download failed") from None

    return response.json()
```

The example selects the first Voice capture with a `vcon-` schema version for the first task in the response. It accepts both `realtime-voice` and `recording` sources, while excluding digital captures. Recognizing the vCon format does not guarantee that your parser supports every version; check the full version value for compatibility before parsing.
