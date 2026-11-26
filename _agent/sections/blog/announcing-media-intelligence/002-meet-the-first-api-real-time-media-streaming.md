---
type: Excerpt
canonical_url: https://developer.webex.com/blog/announcing-media-intelligence
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Meet the first API: Real Time Media Streaming'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/announcing-media-intelligence). [Full Markdown](../../../../blog/announcing-media-intelligence.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Webex generates valuable audio, video, and conversational data. If you build a product, integration, or workflow, Media Intelligence gives you a way to bring Webex media into that experience. As a developer, you can connect your application to Webex, apply the AI, analytics, and processing services that fit your product, and deliver capabilities tailored to your customers and industry.

## Selected section

## Meet the first API: Real Time Media Streaming

Building real-time media features for meetings often requires meeting bots and complex media-processing pipelines. Bots can disrupt the participant experience, while custom pipelines make live media harder to access and increase infrastructure costs. RTMS addresses these challenges by delivering live, structured audio and video streams for individual participants directly to a service you choose—without requiring a bot. This direct access simplifies media processing and avoids unnecessary decoding and re-encoding, reducing processing overhead and infrastructure costs.

RTMS delivers structured, per-participant audio and video, so your application can identify and process each person’s audio separately for greater accuracy, and provide more relevant insights. A privacy-first approach keeps participants informed through clear in-meeting notifications and lets hosts and cohosts enable or disable external streaming.

The integration flow is straightforward:

1. Build or configure your application to receive meeting media.
2. Process the audio and video using the services of your choice.
3. Integrate the results into your new or existing applications or workflows to deliver ready-to-use solutions to your customers.

![Diagram showing the RTMS flow from a Webex meeting through an RTMS session, receiving application, processing, and product action.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1c6b00f8a368cfaf/6ac3eef98695b034d7730a21/rtms-high-level-flow.png)

RTMS is intentionally a building block. This gives you the flexibility to combine Webex meeting media with the AI services and tools you already use or to create the product experiences you want.
