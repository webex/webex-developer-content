---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- BYOVA over gRPC overview
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## BYOVA over gRPC overview

Bring Your Own Virtual Agent (BYOVA) over gRPC uses the published `VoiceVirtualAgent` protobuf contract. Webex Contact Center is the gRPC client, and your connector hosts the gRPC server and adapts your speech and AI services to the Webex media and event model.

The service exposes two RPCs:

| RPC | Purpose |
| --- | --- |
| `ProcessCallerInput` | Bidirectional stream for caller audio, DTMF, input events, prompts, and output events. |
| `ListVirtualAgents` | Unary request that returns the virtual agents available to an organization. |

Use the published [Voice Virtual Agent protobuf definitions](https://github.com/webex/dataSourceSchemas/tree/main/Services/VoiceVirtualAgent_5397013b-7920-4ffc-807c-e8a3e0a18f43/Proto) as the source of truth for message fields and enum values. The [CiscoDevNet gRPC connector samples](https://github.com/CiscoDevNet/webex-contact-center-provider-sample-code/tree/main/bring-your-own/virtual-agent/grpc-interface) provide Java and Python reference implementations.
