---
type: Article
title: 'More ways to connect voice AI: WebSocket support for Webex BYOVA'
canonical_url: https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket
content_type: blog
date: '2026-11-04'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/connect-voice-ai-with-webex-byova-websocket)

Webex Contact Center now supports WebSocket for Bring Your Own Virtual Agent (BYOVA), alongside the existing gRPC interface.

If your voice AI already supports WebSocket, you can now use that protocol to connect it to Webex Contact Center through BYOVA. You can choose the interface that fits your voice AI and development stack.

## Choose your connection

Both interfaces support caller audio, virtual-agent responses, DTMF, conversation events, and transfer to a human agent. They differ in message format and how they carry each interaction.

| Aspect | BYOVA over gRPC | BYOVA over WebSocket |
|---|---|---|
| Message format | Protobuf messages | JSON text messages, with audio encoded as Base64 |
| Interaction lifecycle | A new bidirectional `ProcessCallerInput` RPC for each logical interaction | One connection carries multiple turns throughout the conversation |
| Development approach | Protobuf definitions and generated code | WebSocket libraries and schema-defined JSON messages |

Your connector still adapts your voice AI to the Webex requirements for audio, conversation events, turn completion, interruptions, and handoff. See the [gRPC guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc) and [WebSocket guide](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket) for each contract.

## Start with Java or Python

Sample code is available in both languages:

- [Java WebSocket sample](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/web-socket-interface/simulators/byova-websocket-json-java): A Spring Boot implementation covering conversation and virtual-agent discovery endpoints, audio and event handling, and handshake authentication.
- [Python BYOVA gateway](https://github.com/webex/webex-byova-gateway-python): A gateway supporting gRPC and WebSocket, with connectors for external voice-agent services. Follow its [WebSocket setup guide](https://github.com/webex/webex-byova-gateway-python/blob/main/docs/WEBSOCKET_TRANSPORT.md) to configure the interface.

These are samples for building and evaluating an integration. You or your implementation partner own the adaptation, hosting, security, capacity, and operations of your deployment.

## Make your first test call

[Create a Webex Contact Center Developer Sandbox](https://developer.webex.com/create/docs/sandbox_cc), which includes a BYOVA test license. Follow the [BYOVA setup](https://developer.webex.com/docs/bring-your-own-virtual-agent) to confirm Voice Virtual Agent entitlements are enabled before configuring your flow. If they aren’t enabled, request them through [Developer Support](https://developer.webex.com/support). Connect your voice AI using the Java or Python sample, then test a conversation with interruption and handoff.
