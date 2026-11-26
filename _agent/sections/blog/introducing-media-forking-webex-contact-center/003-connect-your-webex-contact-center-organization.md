---
type: Excerpt
canonical_url: https://developer.webex.com/blog/introducing-media-forking-webex-contact-center
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Connect your Webex Contact Center organization
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/blog/introducing-media-forking-webex-contact-center). [Full Markdown](../../../../blog/introducing-media-forking-webex-contact-center.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Media Forking gives developers and technology partners access to a live copy of caller and agent audio from Webex Contact Center. Your application receives the audio while the conversation continues and connects it to the speech recognition, analytics, or other processing services you choose.

A *media stream* carries the call’s audio. *Forking* sends a copy to an external application, called a receiver. That receiver is where your integration begins: it accepts the audio and passes it to your processing code or connected services.

## Selected section

## Connect your Webex Contact Center organization

Start with the [WebexSamples Node.js receiver](https://github.com/WebexSamples/webex-contact-center-media-forking-sample) and a Webex Contact Center organization with the Media Forking subscription entitlement.

The setup connects your organization, receiver, and call flow:

1. **Authorize the integration.** Create a Service App with the data-source scopes and Media Forking schema. Have a Full Admin authorize it for your organization.
2. **Configure the receiver and registration.** Prepare a publicly reachable gRPC endpoint with a trusted TLS certificate. Register it through the Data Sources API and configure the receiver with the corresponding organization and data-source bindings.
3. **Start streaming from your flow.** In the inbound flow’s **AgentAccepted** event handler, add **Start Media Stream** and select the authorized Service App as the media destination. Validate and publish the flow.
4. **Verify a real conversation.** Place a call through that flow and have an agent answer. Confirm that the receiver accepts authenticated streams, receives caller and agent audio, and completes processing when the call ends.

Once audio reaches the receiver, extend its audio handler to connect your speech recognition or analytics service. You can also enable optional WAV recording to inspect captured audio, with appropriate storage access and retention controls.

Read the [Media Forking overview](https://developer.webex.com/webex-contact-center/docs/media-forking-overview), then follow the [implementation guide](https://developer.webex.com/webex-contact-center/docs/media-forking-guide) for registration, receiver configuration, and call-validation steps.
