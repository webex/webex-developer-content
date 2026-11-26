---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guide-for-contact-center-transcripts
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Known Limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guide-for-contact-center-transcripts). [Full Markdown](../../../../docs/guide-for-contact-center-transcripts.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide explains how to find and parse Voice vCon transcript JSON returned through the Captures API. It focuses on the transcript file format; use the [Captures API reference](https://developer.webex.com/webex-contact-center/docs/api/v1/captures/list-captures) for endpoint details, authorization, request fields, limits, and the full response schema.

---

Voice vCon transcripts may contain conversations between:

- an AI Agent and a user
- a Human Agent and a user
- multiple AI Agents, Human Agents, and a user

The transcript file uses the `vcon` schema, which is based on the [vCon Conversation Data Container draft (revision 04)](https://datatracker.ietf.org/doc/html/draft-ietf-vcon-vcon-core-04). In this format, participants are represented in the top-level `parties` array and transcript messages are represented in the top-level `dialog` array.

## Selected section

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
