---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Try the receiver sample
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Try the receiver sample

The [WebexSamples Node.js receiver](https://github.com/WebexSamples/webex-contact-center-media-forking-sample) provides TLS and JWS validation, the media and health RPCs, bounded audio handling, and optional WAV recording. Start with its synthetic demo before connecting an organization.

Install Node.js 24, then run:

```sh
git clone https://github.com/WebexSamples/webex-contact-center-media-forking-sample.git
cd webex-contact-center-media-forking-sample
npm ci
npm run demo
```

Expect `media_received` logs for `CALLER` and `AGENT`, `stream_completed`, and `Demo passed`. The demo sends distinct one-second synthetic tones over loopback, verifies a final `SUCCESS`, and checks that an unauthenticated stream is rejected. It needs no Webex organization or credentials. Its temporary keys and plaintext loopback transport are confined to the demo; `npm start` requires TLS and Webex JWS validation.

For a real organization, follow the [sample setup walkthrough](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/docs/SETUP.md) and the registration and flow steps below. Copy `.env.example` to `.env`, set the registered data-source bindings and TLS certificate/key paths, and run `npm start`. The receiver requires TLS 1.3 and an HTTP/2-capable public network path. Keep credentials and tenant configuration out of source control.

Add your processing in [`lib/audio.mjs`](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/lib/audio.mjs). The handler receives validated, normalized non-empty audio and an `AbortSignal`; honor cancellation and set downstream timeouts. The starter accepts one configured customer organization and data source per process. Its [validation notes](https://github.com/WebexSamples/webex-contact-center-media-forking-sample/blob/main/docs/VALIDATION.md) distinguish synthetic checks, live SDK calls, and remaining coverage; the sample is not certified for production capacity or reliability.
