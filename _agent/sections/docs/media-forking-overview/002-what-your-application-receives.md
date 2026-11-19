---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- What your application receives
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## What your application receives

Media Forking delivers audio and the metadata needed to identify and interpret it:

- **Caller and agent audio:** The streams identify the speaker as `CALLER` or `AGENT`, so your application can process each side separately and associate the results with the speaker.
- **Conversation context:** Conversation, organization, and participant metadata let your receiver associate incoming media with the call and its participants.
- **Audio format:** Encoding and sample-rate metadata tell your receiver how to interpret the raw audio bytes.

Your application turns these inputs into the outputs it needs. A transcript requires speech recognition; a summary requires further processing of the conversation; an audio file requires the receiver to write the received audio in a suitable file format. The sample receiver demonstrates media receipt and optional WAV recording.
