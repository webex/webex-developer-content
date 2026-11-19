---
type: Guide
title: Media Forking | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/media-forking-overview
content_type: documentation
product_group:
- webex-contact-center
categories:
- mcp
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/media-forking-overview)

**Media Forking** sends a live copy of caller and agent audio from a Webex Contact Center call to an external application. It gives developers access to the conversation as it happens so they can build applications that process speech during the call.

## Media Forking Overview

A *media stream* carries a call's audio. *Forking* sends a copy of that stream to another application while the call continues.

The application that receives this copy is the *media receiver*. You can run it yourself or use a partner's service. The receiver accepts the streamed audio and passes it to your processing code or to services you choose, such as a speech recognition service.

This lets you build around a live caller-agent conversation. For example, your application can transcribe speech as it arrives, use the transcript to look up relevant information, and display that information in an agent-facing application. You decide how to process the audio and where to use the results.

## What your application receives

Media Forking delivers audio and the metadata needed to identify and interpret it:

- **Caller and agent audio:** The streams identify the speaker as `CALLER` or `AGENT`, so your application can process each side separately and associate the results with the speaker.
- **Conversation context:** Conversation, organization, and participant metadata let your receiver associate incoming media with the call and its participants.
- **Audio format:** Encoding and sample-rate metadata tell your receiver how to interpret the raw audio bytes.

Your application turns these inputs into the outputs it needs. A transcript requires speech recognition; a summary requires further processing of the conversation; an audio file requires the receiver to write the received audio in a suitable file format. The sample receiver demonstrates media receipt and optional WAV recording.

## What you can build

- **Live transcription:** Send the audio to a speech recognition service and display the resulting text in your application while the call is in progress. Keep caller and agent text associated with the corresponding speaker.
- **Agent assistance:** Use a transcript to search a knowledge base or generate suggested responses. Present the results in your agent-facing application so the agent can use them during the conversation.
- **Conversation analysis:** Process transcripts to identify topics, keywords, or sentiment. Use the results to generate call summaries or feed your own review and follow-up workflows.
- **Audio capture:** Save received audio for later playback or processing. Your receiver controls the file format and storage; your application must manage access and retention.

These workflows run in the receiver and its connected services. You can begin by receiving audio, then add the speech or analysis service your application needs.

## Subscription requirement

The customer organization must have the Media Forking offer (`MFCS`) on its Webex Contact Center subscription. The orderable SKUs are `A-FLEX-MEDSTRM` (Flex 3) and `E3CE-MEDSTRM` (Enterprise Agreement). For Flex 3 ordering details, see the [ordering guide](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-og.html) and [data sheet](https://www.cisco.com/c/en/us/products/collateral/customer-collaboration/collab-flex-3-contact-center-ds.html).

## How it works

When **Start Media Stream** runs for an answered caller-agent conversation, Webex Contact Center establishes a gRPC connection to the registered partner endpoint. Webex Contact Center acts as the gRPC client, and the partner endpoint acts as the gRPC server.

Use a publicly reachable TLS endpoint. Each media RPC carries a signed JWS in the gRPC `authorization` metadata; validate it before processing audio.

![Webex Contact Center copies caller and agent audio over TLS to an external gRPC receiver that validates the JWS and can run custom processing or optional WAV recording.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5ce44070d2255496/6aee2168d18c220b0f50eacd/media-forking-overview.jpg)

1. After the agent answers, Flow Designer runs **Start Media Stream** with the authorized Service App selected as the media destination. For an inbound flow, connect it to the **AgentAccepted** event handler.
2. Webex Contact Center opens a bidirectional gRPC stream to the registered partner endpoint. Caller and agent media can arrive on separate RPCs.
3. The client sends conversation audio in `ConversationAudioForkingRequest` messages.
4. The receiver sample waits for the client to half-close the request stream and finishes processing queued audio. It then sends one final `ConversationAudioForkingResponse` per RPC and closes that response stream. The response can contain acknowledgment, status, or error information.

Although the RPC is bidirectional, the response carries processing status; it does not provide a way for the receiver to send voice back into the call.

For queue-specific conditional logic in Flow Designer, see [Enabling media streaming for specific queues](https://help.webex.com/en-us/article/n5jhgdi/Enabling-media-streaming-for-specific-queues) in the Webex Help Center.

## Media stream

Opening messages can contain conversation, organization, participant, and format metadata before any audio arrives. Later audio packets can omit the organization, encoding, and sample rate; retain the validated opening metadata for that leg. Preserve a capture timestamp when supplied and leave it absent when omitted.

The stream carries variable-sized raw mono audio at 8000 or 16000 Hz, without a WAV header.

The `CALLER` and `AGENT` roles identify the source of each stream. The schema defines `LINEAR16`, `MULAW`, and `ALAW` audio encodings. How the endpoint stores or processes the raw audio is implementation-specific.

## Get started

Start with the [WebexSamples Node.js receiver](https://github.com/WebexSamples/webex-contact-center-media-forking-sample) to learn the connection lifecycle, receive separate caller and agent audio, and optionally save WAV files. Its synthetic demo runs without a Webex organization. Extend its audio handler to add your own processing. The [CiscoDevNet provider sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/media-forking) is the protocol reference.

Follow the [Media Forking guide](https://developer.webex.com/mcp/docs/media-forking-guide) to run the sample, authorize a Service App, register the data source, configure the flow, and verify media receipt. The guide also explains optional WAV recording. Recording is implemented by the sample and stays off by default; storing call audio requires private storage, encryption, and an explicit retention policy.
