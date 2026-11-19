---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Breaking changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

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
