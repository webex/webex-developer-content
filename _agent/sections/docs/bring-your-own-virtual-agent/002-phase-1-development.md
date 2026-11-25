---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Phase 1 - Development
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent). [Full Markdown](../../../../docs/bring-your-own-virtual-agent.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Phase 2 - Authentication](003-phase-2-authentication.md)

## Article introduction

As part of the "Bring Your Own" (BYO) initiative, Webex Contact Center aims to enable seamless integrations with third-party AI providers, enhancing the Webex customer experience with cutting-edge AI innovations. Bring your own Virtual Agent is the first slice of all other other AI functionalities you can bring to Webex Contact Center product offerings.

## Selected section

## Phase 1 - Development 

**Dialog Connector Simulator**

![VA Provisioning](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf3590174c4a89d3c/6914d8e3424c33f4acbca376/VAProvisioning.jpg?branch=integration)

*Fig 2: Architectural Diagram for provisioning an Virtual Agent*

The Dialog Connector Simulator is a sample Java application that demonstrates how to integrate an external conversational interface with Webex Contact Center IVR. Refer to the [Dialog Connector Simulator Sample Code](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code) for guidance.

All media from Universal Harness (media platform) is streamed using [gRPC APIs](https://grpc.io), and the Virtual Agent APIs use [bidirectional streaming](https://grpc.io/docs/what-is-grpc/core-concepts/) to send and receive media from the 3rd party provider.

For implementation details, see [BYOVA over gRPC](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). If you are using the JSON transport instead, see [BYOVA over WebSocket](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-websocket).

For the gRPC variant, you can optionally [enable mTLS authentication](https://developer.webex.com/docs/bring-your-own-virtual-agent-mtls-authentication) to add transport-layer client authentication. mTLS does not apply to the WebSocket variant and does not replace the existing JWS/JWT validation.

1. Start by getting yourself a [Webex Contact Center Sandbox](https://developer.webex.com/docs/sandbox_cc).
1. Request Voice Virtual Agent entitlements via [developer support](https://developer.webex.com/support).
1. Go through the [protobuf definition](https://github.com/webex/dataSourceSchemas/tree/v1.2/Services/VoiceVirtualAgent_5397013b-7920-4ffc-807c-e8a3e0a18f43).
1. Sample Code: https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code

Catch the code walkthrough demo here: https://app.vidcast.io/share/41f3d470-07cc-412d-bd50-d5c9e00d3183?playlistShareId=1f4a2dff-8be4-4dd5-a1fb-d5aae8441bd3&autoplay=1


**Note: Start testing in the cloud sandbox, and the same service app can be used for testing on a CCE test setup for validation.**
