---
type: Guide
title: Migrating to Voice vCon Transcripts
display_title: Migrating to Voice vCon Transcripts
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts)

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Who needs to migrate

Any application that currently downloads or reads the legacy `voiceTranscript.json` file from the Captures API needs to migrate.

This includes applications that select transcript captures using metadata such as `source: "recording"` or `fileName: "voiceTranscript.json"`, as well as applications that parse the downloaded transcript payload under `responseContents[]`. Recording-derived vCon transcripts can retain that source and file name, so those values alone no longer identify the legacy format.

## Migration at a glance

Most consumers need to make these changes:

1. Select Voice captures with `source: "realtime-voice"` or `source: "recording"`, then check whether `transcriptSchemaVersion` starts with `vcon-` to identify the vCon format.
2. Download the selected capture using `filePath`. The file may be `realtimeVoiceTranscript.json` or a recording-derived `voiceTranscript.json`.
3. Iterate through `dialog[]` instead of `responseContents[]`.
4. Read transcript text from `dialog[].body`.
5. Resolve the speaker through `parties[dialog[].originator]`.
6. Handle `customer`, `agent`, and `virtual-agent` roles.
7. Make legacy-only fields such as `alternatives`, `confidence`, and `words[]` optional or remove those dependencies.

If your application primarily displays, stores, searches, or summarizes transcript text, the main parser change is moving from `responseContents[].recognitionResult.alternatives[0].transcript` to `dialog[].body`, with speaker role resolved through `parties[]`.

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

## Breaking changes

### 1. Transcript entries moved from `responseContents` to `dialog`

Legacy consumers usually iterate over:

```python
payload["responseContents"]
```

Voice vCon transcript consumers should iterate over:

```python
payload["dialog"]
```

Each `dialog` item represents a text entry in the conversation. The transcript text is available in `dialog[].body`.

### 2. Speaker role is now resolved through `parties`

In the legacy format, the speaker role was embedded directly on each recognition result:

```json
{
  "recognitionResult": {
    "role": "CALLER"
  }
}
```

In the Voice vCon format, each dialog entry contains an `originator` index. Resolve that index against the top-level `parties` array:

```python
entry = payload["dialog"][0]
speaker = payload["parties"][entry["originator"]]
```

Current role mapping:

| Represents | Legacy role | Voice vCon party role |
| --- | --- | --- |
| Customer | `CALLER` | `customer` |
| Human Agent | `AGENT` | `agent` |
| AI Agent | No legacy equivalent | `virtual-agent` |

The `virtual-agent` role is new in the Voice vCon format and represents AI Agents. Do not hard-code party indexes. In the current sample, `0` is the customer and `1` is the AI Agent, but consumers should always resolve the role through `parties[dialog.originator]`.

### 3. Transcript text is now read from `dialog[].body`

Legacy:

```python
text = item["recognitionResult"]["alternatives"][0]["transcript"]
```

Voice vCon:

```python
text = entry["body"]
```

The Voice vCon format exposes the finalized transcript text in the `body` field of each `dialog[]` object. Consumers no longer need to choose from an `alternatives` array.

### 4. Timing changed from word-level call offsets to dialog-level start time

The legacy format does not provide a message-level timestamp. It provides per-word timing offsets that indicate when each word was spoken within the call or audio stream:

```json
{
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
```

The Voice vCon format provides a dialog-entry start time as an absolute ISO 8601 timestamp:

```json
{
  "start": "2026-04-28T11:59:37.459Z"
}
```

Use `dialog[].start` when entry-level timing is sufficient. If your application requires word-level start and end offsets, note that the Voice vCon sample does not include a direct replacement for `words[]`.

### 5. Confidence scores are not present in the Voice vCon sample

The legacy format included recognition confidence at:

```python
item["recognitionResult"]["alternatives"][0]["confidence"]
```

The Voice vCon sample does not include an equivalent confidence field. Consumers should remove confidence-score dependencies, make the field optional, or source confidence data from a separate API if available.

### 6. Language moved to `language`

Legacy:

```json
{
  "languageCode": "en-US"
}
```

Voice vCon:

```json
{
  "language": "en-US"
}
```

The legacy per-result `recognitionResult.language_code` is also replaced by the top-level Voice vCon `language` field.

## Quick field mapping

| Represents | Legacy field | Voice vCon field | Notes |
| --- | --- | --- | --- |
| Transcript identifier | `interactionId` | `uuid` | Use `uuid` as the top-level Voice vCon transcript identifier. It equals `data[].taskId` in the Captures API response. |
| Transcript entries | `responseContents[]` | `dialog[]` | The legacy format stores recognition results. The Voice vCon format stores vCon dialog entries. |
| Transcript text | `responseContents[].recognitionResult.alternatives[0].transcript` | `dialog[].body` | Text is in the `body` field of each `dialog[]` object. |
| Speaker role | `responseContents[].recognitionResult.role` | `parties[dialog[].originator].role` | Resolve the `originator` index against `parties[]` to identify the speaker. |
| Transcript language metadata | `languageCode`, `recognitionResult.language_code` | `language` | Language metadata is available at the top level. |
| Entry timing | `words[].start_time`, `words[].end_time` | `dialog[].start` | Legacy timing is word-level call offset timing. Voice vCon timing is dialog-level absolute timestamp. |
| Recognition confidence | `alternatives[0].confidence` | No direct equivalent | Make optional or remove this dependency. |
| Session identifier | Not available | `dialog[].session_id.local` | AI Agent session ID for AI Agent dialogs; interaction ID for recording-derived Human Agent transcripts. `segment_id` may remain as a compatibility fallback. |

## Recommended migration approach

### Step 1: Check transcript format using `transcriptSchemaVersion`

During rollout, support both formats if existing stored transcripts may still use the legacy schema. Legacy recording captures lack `transcriptSchemaVersion`; Voice vCon captures always include it. First restrict selection to `source: "realtime-voice"` or `source: "recording"`, then check whether `transcriptSchemaVersion` starts with `vcon-`, rather than matching a fixed version number.

```python
def get_transcript_format(transcription_item):
    source = transcription_item.get("source")

    if source not in {"realtime-voice", "recording"}:
        return "unknown"

    schema_version = transcription_item.get("transcriptSchemaVersion")

    if schema_version:
        return "vcon" if schema_version.startswith("vcon-") else "unknown"

    return "legacy" if source == "recording" else "unknown"
```

After downloading the transcript file, validate its shape before choosing a parser: legacy files contain `responseContents[]`, while Voice vCon files contain `dialog[]` and `parties[]`.

Recognizing the vCon format does not guarantee support for every version. Use the full version value to check parser compatibility.

### Step 2: Read Voice vCon transcript entries directly

In the Voice vCon format, each transcript message is available directly in `dialog[]`. Read message text from `dialog[].body`, dialog entry start time from `dialog[].start`, and speaker details from `parties[dialog[].originator]`.

```python
parties = payload.get("parties") or []

for dialog_entry in payload.get("dialog") or []:
    originator = dialog_entry.get("originator")

    if isinstance(originator, int) and 0 <= originator < len(parties):
        speaker = parties[originator]
    else:
        speaker = {}

    timestamp = dialog_entry.get("start")
    speaker_role = speaker.get("role")
    speaker_id = speaker.get("uuid")
    text = dialog_entry.get("body")
    session_id = dialog_entry.get("session_id")
    session_identifier = (
        session_id.get("local") if isinstance(session_id, dict) else None
    ) or dialog_entry.get("segment_id")

    print(timestamp, speaker_role, speaker_id, text, session_identifier)
```

For the session identifier, prefer `dialog[].session_id.local`. The vCon [session identifier model](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04#section-4.3.12) uses an object; do not pass the whole `session_id` value to code that expects a string. The example falls back to `segment_id` for older transcripts. Recording-derived Human Agent transcripts use the interaction ID as the local identifier.

### Step 3: Update role handling

If your application expects legacy role values, map Voice vCon party roles at your integration boundary:

```python
VCON_TO_LEGACY_ROLE = {
    "customer": "CALLER",
    "agent": "AGENT",
}


def get_legacy_compatible_role(payload, dialog_entry):
    parties = payload.get("parties") or []
    originator = dialog_entry.get("originator")

    if isinstance(originator, int) and 0 <= originator < len(parties):
        role = parties[originator].get("role")
    else:
        role = None

    return VCON_TO_LEGACY_ROLE.get(role, role or "UNKNOWN")
```

For new code, prefer the Voice vCon role values directly.

The `virtual-agent` role has no legacy role equivalent. Do not treat `virtual-agent` as legacy `AGENT`; legacy `AGENT` refers to a Human Agent and maps to Voice vCon `agent`.

## Rollout checklist

Before rollout, verify the following:

- Format detection restricts selection to `realtime-voice` or `recording` sources and checks the `vcon-` prefix in `transcription[].transcriptSchemaVersion`; the parser validates the downloaded payload shape and supported version. `source` and `fileName` alone are insufficient for recording-derived transcripts.
- Session handling reads `dialog[].session_id.local`, tolerates an absent `remote`, and falls back to `segment_id` when needed.
- Speaker handling resolves `originator` through `parties[]` and does not assume fixed party indexes.
- Role handling treats `agent` as the Human Agent role and `virtual-agent` as the AI Agent role.
- `parties[].uuid`, confidence scores, alternatives, and word-level timings are optional.
- Tests cover AI Agent-only, Human Agent-only, and AI Agent plus Human Agent conversations.
- Analytics, redaction, search, export, and UI code read transcript content from `dialog[]`, `dialog[].body`, and `parties[dialog[].originator]`.

## Compatibility recommendation

For the safest rollout, support both formats during the migration window and update downstream consumers to read the Voice vCon transcript fields directly. Once all stored transcripts and API responses use the Voice vCon format, remove the legacy parser and any dependencies on confidence scores, recognition alternatives, and word-level offsets.
