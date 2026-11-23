---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-overview
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Get started
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-overview). [Full Markdown](../../../../docs/media-forking-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Subscription requirement](004-subscription-requirement.md)

## Article introduction

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Selected section

## Get started

Start with the [WebexSamples Node.js receiver](https://github.com/WebexSamples/webex-contact-center-media-forking-sample) to learn the connection lifecycle, receive separate caller and agent audio, and optionally save WAV files. Its synthetic demo runs without a Webex organization. Extend its audio handler to add your own processing. The [CiscoDevNet provider sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/media-forking) is the protocol reference.

Follow the [Media Forking guide](https://developer.webex.com/mcp/docs/media-forking-guide) to run the sample, authorize a Service App, register the data source, configure the flow, and verify media receipt. The guide also explains optional WAV recording. Recording is implemented by the sample and stays off by default; storing call audio requires private storage, encryption, and an explicit retention policy.
