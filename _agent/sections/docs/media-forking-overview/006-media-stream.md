---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Media stream
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## Media stream

Opening messages can contain conversation, organization, participant, and format metadata before any audio arrives. Later audio packets can omit the organization, encoding, and sample rate; retain the validated opening metadata for that leg. Preserve a capture timestamp when supplied and leave it absent when omitted.

The stream carries variable-sized raw mono audio at 8000 or 16000 Hz, without a WAV header.

The `CALLER` and `AGENT` roles identify the source of each stream. The schema defines `LINEAR16`, `MULAW`, and `ALAW` audio encodings. How the endpoint stores or processes the raw audio is implementation-specific.
