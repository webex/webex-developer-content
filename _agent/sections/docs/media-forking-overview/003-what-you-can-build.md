---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- What you can build
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## What you can build

- **Live transcription:** Send the audio to a speech recognition service and display the resulting text in your application while the call is in progress. Keep caller and agent text associated with the corresponding speaker.
- **Agent assistance:** Use a transcript to search a knowledge base or generate suggested responses. Present the results in your agent-facing application so the agent can use them during the conversation.
- **Conversation analysis:** Process transcripts to identify topics, keywords, or sentiment. Use the results to generate call summaries or feed your own review and follow-up workflows.
- **Audio capture:** Save received audio for later playback or processing. Your receiver controls the file format and storage; your application must manage access and retention.

These workflows run in the receiver and its connected services. You can begin by receiving audio, then add the speech or analysis service your application needs.
