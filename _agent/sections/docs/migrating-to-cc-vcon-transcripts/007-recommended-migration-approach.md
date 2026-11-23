---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Recommended migration approach
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

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
