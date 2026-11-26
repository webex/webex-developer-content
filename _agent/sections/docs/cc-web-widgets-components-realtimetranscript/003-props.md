---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Props
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-realtimetranscript). [Full Markdown](../../../../docs/cc-web-widgets-components-realtimetranscript.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `RealTimeTranscript` component renders the live voice transcript for the currently selected task.

## Selected section

## Props

| Prop | Type | Required | Description |
| --- | --- | --- | --- |
| `className` | `string` | No | Adds a custom CSS class to the root container. |
| `liveTranscriptEntries` | `RealTimeTranscriptEntry[]` | No | Optional fallback transcript entries to render when live store-backed transcript data is not available. |

### RealTimeTranscriptEntry

| key | type | description |
| --- | --- | --- |
| `id` | `string` | Unique entry identifier. |
| `speaker` | `string` | Speaker label shown in the transcript UI. |
| `message` | `string` | Transcript text for the entry. |
| `timestamp` | `number` | Timestamp used for sorting transcript entries. |
| `displayTime` | `string` | Optional formatted time label. |
| `event` | `string` | Optional event label rendered above the transcript line. |
| `isCustomer` | `boolean` | Marks the entry as customer speech for avatar styling. |
| `avatarUrl` | `string` | Optional avatar image URL. |
| `initials` | `string` | Optional avatar initials fallback. |
