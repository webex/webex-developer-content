---
type: Excerpt
canonical_url: https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Quick field mapping
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/migrating-to-cc-vcon-transcripts). [Full Markdown](../../../../docs/migrating-to-cc-vcon-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to migrate API consumers from Legacy Voice Transcript Format to Voice vCon Transcript Format. The legacy transcript format represents only the Human Agent to customer leg of a conversation. The Voice vCon transcript format can represent the full Contact Center conversation, including AI Agents, Human Agents, and customers in the same interaction.

---

The legacy format stores transcript output as speech recognition results under `responseContents`. The Voice vCon format stores the conversation as a vCon-style document with top-level conversation metadata, participants, and dialog entries. For the complete object model, refer to the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04).

## Selected section

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
