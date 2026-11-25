---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Record WAV audio with the sample
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Record WAV audio with the sample

Media Forking supplies raw audio; the Node.js sample can wrap received bytes in a WAV container without transcoding. Recording is disabled by default. To try it with synthetic caller and agent tones:

```sh
RECORDING_DIR=./recordings npm run demo
```

![The optional recorder wraps raw audio in separate caller and agent WAV files, writes partial files, then finalizes the header, syncs, closes and renames each file.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5f50f2625ddea0f5/6aee21e56c10e6d96b818394/wav-recording-output.jpg)

*Caller and agent labels illustrate separate outputs. Actual filenames include generated stream, leg, and segment identifiers.*

To record real incoming streams, set `RECORDING_DIR=./recordings` in `.env` and run `npm start`. Each RPC/participant leg gets a separate mono WAV file using its declared `LINEAR16`, `MULAW`, or `ALAW` encoding at 8000 or 16000 Hz. Use a player that supports the codec. Reconnects create new files; format changes start new segments. Files retain arrival order without mixing participants, filling gaps, or aligning timestamps.

Look for `recording_saved` followed by `stream_completed`. The writer finalizes the header, syncs and closes the file, then renames `.wav.partial` to `.wav` before acknowledging success. Cancellation can still produce a valid WAV covering only part of a call; check `stream_failed` as well. A crash or disk error can leave `.partial` files, which the sample does not recover automatically.

The sample requires a private, writable recording directory (`0700`) and creates files with mode `0600`. Keep recordings outside web-served paths, use encrypted storage, monitor available space, and define a retention/cleanup policy. Disk exhaustion fails the stream. See [recording behavior and limits](https://github.com/WebexSamples/webex-contact-center-media-forking-sample#record-wav-audio) before enabling capture.
