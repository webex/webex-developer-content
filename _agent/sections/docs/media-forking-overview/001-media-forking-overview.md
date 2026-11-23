---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Media Forking Overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## Media Forking Overview

A *media stream* carries a call's audio. *Forking* sends a copy of that stream to another application while the call continues.

The application that receives this copy is the *media receiver*. You can run it yourself or use a partner's service. The receiver accepts the streamed audio and passes it to your processing code or to services you choose, such as a speech recognition service.

This lets you build around a live caller-agent conversation. For example, your application can transcribe speech as it arrives, use the transcript to look up relevant information, and display that information in an agent-facing application. You decide how to process the audio and where to use the results.
