---
type: Guide
title: Guide for Voice Transcripts
display_title: Guide for Voice Transcripts
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/guide-for-contact-center-transcripts)

This guide explains how to find and parse Voice vCon transcript JSON returned through the Captures API. It focuses on the transcript file format; use the [Captures API reference](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) for endpoint details, authorization, request fields, limits, and the full response schema.

---

Voice vCon transcripts may contain conversations between:

- an AI Agent and a user
- a Human Agent and a user
- multiple AI Agents, Human Agents, and a user

The transcript file uses the `vcon` schema, which is based on the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04). In this format, participants are represented in the top-level `parties` array and transcript messages are represented in the top-level `dialog` array.

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

## Participants and Roles

Participants in a Voice vCon transcript are listed in `parties`, following the vCon [party object](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-4.2) model. Each dialog entry identifies its speaker through the `originator` index.

For example:

```json
{
  "parties": [
    {
      "role": "customer"
    },
    {
      "uuid": "69e23483c39ab81f25fa9bc8",
      "role": "virtual-agent"
    },
    {
      "uuid": "4f854080-9497-4b3d-aa4f-a406d0d6f8bd",
      "role": "agent"
    }
  ]
}
```

Allowed participant roles:

| Role | Description |
| --- | --- |
| `customer` | The end user or caller. |
| `virtual-agent` | The AI Agent participating in the conversation. |
| `agent` | The Human Agent participating in the conversation. |

Possible transcript participant combinations:

| Conversation type | Example roles in `parties` |
| --- | --- |
| AI Agent and user | `customer`, `virtual-agent` |
| Human Agent and user | `customer`, `agent` |
| AI Agent, Human Agent, and user | `customer`, `virtual-agent`, `agent` |

Do not assume a fixed party index for a role. Always resolve the speaker by reading:

```python
party = transcript["parties"][dialog_entry["originator"]]
```

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

## Known Limitations

The following limitations may be observed when consuming Voice vCon transcripts.

| Limitation | Consumer guidance |
| --- | --- |
| In complex escalation flows, such as AI Agent to Human Agent transfer followed by consult and merge, duplicate transcript messages may appear in Voice vCon transcripts. | Consumers should not assume every `dialog[]` entry is unique. If duplicate text is problematic for the consuming application, apply deduplication carefully using timestamp, `originator`, `body`, and `session_id.local` (or `segment_id` for older transcripts) rather than text alone. |
| For unsupported languages in the Agent Assist flow, transcript language metadata may default to `en-US` after transfer to a Human Agent. | Treat `language` and capture-level `languageCode` as transcript metadata, not guaranteed language detection for every utterance. Document supported-language behavior in user-facing integrations. |
| Transcript text and message order may differ between the Contact Center Session UI and Voice vCon transcripts. API transcripts may include finalized speech-to-text output with punctuation and formatting, while the Session UI may show lower-latency, non-final text. When a customer barges in during an AI Agent response, the Session UI may show only the partial response that was played, while the API transcript may contain the full generated AI Agent response. In some flows that use custom events, transcript messages may appear in a different order from the Session UI. | Use the API transcript as the persisted transcript source for integrations. Avoid strict string equality comparisons between Session UI text and API transcript text, especially for interrupted AI Agent responses. Do not assume the API transcript and Session UI use the same message order. |
| In rare cases where a participant disconnects immediately after a final utterance, especially in AI Agent to Human Agent flows, the final spoken turn may be absent from the transcript JSON even when the recording contains the audio. | Treat `dialog[]` as the persisted transcript available at capture time, not as a guaranteed complete representation of every recorded audio frame. For workflows that require verification of the final spoken words, use the recording as a reference or account for a possible missing final turn. |
| Long user utterances with pauses may be split into multiple `dialog[]` entries rather than represented as a single user turn. | Treat `dialog[]` entries as transcript segments or utterances, not necessarily complete conversational turns. Merge adjacent entries only if the application has a clear turn-reconstruction requirement. |
| In interactions that move from AI Agent 1 to a Human Agent, then to a consult with AI Agent 2, and then back to the main conversation, `originator` values may not always reflect the expected participant after consult transitions. | Always resolve `originator` through `parties`, but be aware that consult and resume flows may have participant-mapping ambiguity. Consider displaying participant role and timestamp context rather than relying only on index transitions. |
| During a Human Agent consult with AI Agent 2, transcript originators may show the customer and AI Agent 2 instead of the Human Agent and AI Agent 2. | Integrations that analyze consult conversations should account for possible role ambiguity in this flow. |
| Voice vCon transcripts do not currently include conversation content from Google Dialogflow ES or CX integrations. | Do not assume the downloaded vCon transcript includes the Dialogflow portion of an interaction. Account for this gap when displaying or analyzing transcripts. |
