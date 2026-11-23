---
type: Excerpt
canonical_url: https://developer.webex.com/blog/introducing-media-forking-webex-contact-center
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Put live conversations to work
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/introducing-media-forking-webex-contact-center). [Full Markdown](../../../../blog/introducing-media-forking-webex-contact-center.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Media Forking gives developers and technology partners access to a live copy of caller and agent audio from Webex Contact Center. Your application receives the audio while the conversation continues and connects it to the speech recognition, analytics, or other processing services you choose.

A *media stream* carries the call’s audio. *Forking* sends a copy to an external application, called a receiver. That receiver is where your integration begins: it accepts the audio and passes it to your processing code or connected services.

## Selected section

## Put live conversations to work

Consider an agent helping a customer understand an unexpected charge. An application could transcribe the conversation, search a knowledge base for the relevant billing policy, and display suggested information to the agent during the call. Afterward, it could use the transcript to prepare a summary for follow-up.

Other applications could identify recurring topics across conversations or save received audio for later processing. Transcription, summarization, suggested responses, and sentiment analysis are among the uses described in the [Webex Help Center’s media-streaming guidance](https://help.webex.com/en-us/article/n5jhgdi/Enabling-media-streaming-for-specific-queues).

Media Forking supplies the audio and supporting metadata. Your application implements the processing and determines where the results appear. This gives customers and vendors a common connection model for building their own conversation workflows.
