---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Captures API response changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

## Captures API response changes

The Captures API request and top-level response structure do not change because of the transcript format change. Update how your application identifies the format of an item in `data[].transcription[]`, then parse the downloaded file using that format. A recording-derived vCon transcript can retain the legacy source and file name.

The selected entry's `filePath` is a temporary pre-signed URL. Treat it as a temporary credential; do not persist, log, or expose it beyond what is required to download the transcript.

### Captures API response for legacy transcripts

```json
{
  "data": [
    {
      "taskId": "810de9c0-4ad6-455b-96ae-188b8e8bea9a",
      "transcription": [
        {
          "source": "recording",
          "provider": "CISCO",
          "id": "810de9c0-4ad6-455b-96ae-188b8e8bea9a",
          "fileName": "voiceTranscript.json",
          "filePath": "https://{{legacy-transcript-presigned-url}}",
          "startTime": "1778255401389",
          "languageCode": "en-US",
          "configId": "DEFAULT",
          "createTime": "1778255401389"
        }
      ]
    }
  ]
}
```

### Captures API response for Voice vCon transcripts

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
          "filePath": "https://{{vcon-transcript-presigned-url}}",
          "startTime": "1777543415761",
          "languageCode": "ta-IN",
          "configId": null,
          "createTime": "1777543502748",
          "transcriptSchemaVersion": "vcon-04"
        },
        {
          "source": "recording",
          "provider": "CCAI",
          "id": "bb680ea7-7845-4384-8225-76f2b6270075",
          "fileName": "voiceTranscript.json",
          "filePath": "https://{{recording-vcon-transcript-presigned-url}}",
          "languageCode": "en-US",
          "configId": null,
          "transcriptSchemaVersion": "vcon-04"
        }
      ]
    }
  ]
}
```

### Captures API transcription metadata mapping

| Field | Purpose | Change |
| --- | --- | --- |
| `source` | Identifies the transcript production path. | Legacy: `recording`<br>Voice vCon: `realtime-voice` or `recording` |
| `provider` | Identifies the transcription provider. | Legacy: `CISCO`<br>Voice vCon: `CCAI` |
| `fileName` | Identifies the transcript file to download from `filePath`. | Legacy: `voiceTranscript.json`<br>Voice vCon: `realtimeVoiceTranscript.json` or recording-derived `voiceTranscript.json` |
| `configId` | Identifies the transcription configuration when one is associated with the capture. | Legacy: `DEFAULT`<br>Voice vCon: `null` |
| `transcriptSchemaVersion` | Identifies the transcript payload schema version. For Voice sources, check for the `vcon-` prefix to recognize vCon captures. | Legacy: not available<br>Voice vCon: `vcon-*`, for example `vcon-04` |

Use `data[].transcription[]` to locate the transcript file. Restrict selection to Voice sources (`realtime-voice` or `recording`), then check `transcriptSchemaVersion`. Digital captures can also use the `vcon-` prefix:

- A Voice transcription item with `source: "realtime-voice"` or `source: "recording"` and a `transcriptSchemaVersion` starting with `vcon-` identifies a Voice vCon capture, including recording-derived transcripts. Do not require an exact version such as `vcon-04` to recognize the format.
- Voice vCon captures always include `transcriptSchemaVersion`. Do not identify the format using `source` or `fileName` alone; recording-derived vCon transcripts can retain the legacy values.
