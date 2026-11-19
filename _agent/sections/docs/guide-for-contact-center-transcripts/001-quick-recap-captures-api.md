---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Quick Recap - Captures API
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

## Quick Recap - Captures API

Use the Captures API to retrieve capture metadata for one or more Contact Center tasks. The response includes recording metadata and transcription metadata; this guide uses only the transcription metadata needed to find the transcript JSON.

In the Captures response, each item in `data[]` represents a task. Transcript capture metadata is available in `data[].transcription[]`.

Voice vCon transcript captures can use either of these source and file-name combinations:

- `source: "realtime-voice"` with `fileName: "realtimeVoiceTranscript.json"`
- `source: "recording"` with `fileName: "voiceTranscript.json"` for transcripts generated from recordings

For captures with `source: "realtime-voice"` or `source: "recording"`, check whether `transcriptSchemaVersion` starts with `vcon-` to identify the format without requiring a fixed version. Voice vCon captures always include `transcriptSchemaVersion`. Digital captures can also use this prefix, so check both the source and schema version. Current Voice vCon captures use `vcon-04`; `source` and `fileName` alone do not distinguish a recording-derived vCon transcript from a legacy transcript.

The selected entry's `filePath` is a temporary pre-signed URL used to download the transcript JSON.

The example below illustrates both source variants. Available entries depend on the interaction; both are not guaranteed to be present.

```json
{
  "data": [
    {
      "taskId": "bb680ea7-7845-4384-8225-76f2b6270075",
      "transcription": [
        {
          "source": "realtime-voice",
          "provider": "CCAI",
          "id": "bb680ea7-7845-4384-8225-76f2b6270075",
          "fileName": "realtimeVoiceTranscript.json",
          "filePath": "https://{{transcript-presigned-url}}",
          "startTime": "1777377566617",
          "languageCode": "en-US",
          "configId": null,
          "createTime": "1777377653604",
          "transcriptSchemaVersion": "vcon-04"
        },
        {
          "source": "recording",
          "provider": "CCAI",
          "id": "bb680ea7-7845-4384-8225-76f2b6270075",
          "fileName": "voiceTranscript.json",
          "filePath": "https://{{recording-transcript-presigned-url}}",
          "languageCode": "en-US",
          "configId": null,
          "transcriptSchemaVersion": "vcon-04"
        }
      ]
    }
  ]
}
```

Do not persist, log, or expose pre-signed URLs beyond what is required to download the capture. Treat these URLs as temporary credentials.
