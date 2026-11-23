---
type: Excerpt
canonical_url: https://developer.webex.com/blog/introducing-media-forking-webex-contact-center
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect your application to the audio
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/introducing-media-forking-webex-contact-center). [Full Markdown](../../../../blog/introducing-media-forking-webex-contact-center.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Media Forking gives developers and technology partners access to a live copy of caller and agent audio from Webex Contact Center. Your application receives the audio while the conversation continues and connects it to the speech recognition, analytics, or other processing services you choose.

A *media stream* carries the call’s audio. *Forking* sends a copy to an external application, called a receiver. That receiver is where your integration begins: it accepts the audio and passes it to your processing code or connected services.

## Selected section

## Connect your application to the audio

Webex Contact Center connects to your receiver over TLS using gRPC. The stream identifies caller and agent audio and includes conversation, participant, and audio-format metadata. Your application can process each side separately and associate its results with the corresponding speaker.

For an inbound caller-agent conversation, Flow Designer starts streaming after the agent answers, using **Start Media Stream** in the **AgentAccepted** event handler. The activity selects the authorized Service App as the media destination.

Your receiver validates Webex’s signed authorization token before processing audio. From there, you can connect the validated audio to your chosen services and manage the downstream work in your application.
