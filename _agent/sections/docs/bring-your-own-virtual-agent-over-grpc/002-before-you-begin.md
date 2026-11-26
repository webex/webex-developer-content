---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Before you begin
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bring-your-own-virtual-agent-over-grpc). [Full Markdown](../../../../docs/bring-your-own-virtual-agent-over-grpc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Implement a partner-hosted gRPC virtual agent that exchanges caller audio, virtual-agent responses, and conversation events with Webex Contact Center.

## Selected section

## Before you begin

Complete the common Service App, Bring Your Own Data Source (BYODS), Contact Center AI (CCAI), flow, and entry-point provisioning described in [Bring Your Own Virtual Agent](https://developer.webex.com/docs/bring-your-own-virtual-agent).

For the gRPC variant:

1. Implement a publicly reachable TLS-enabled gRPC server before registering the data source.
2. Select Voice Virtual Agent schema ID `5397013b-7920-4ffc-807c-e8a3e0a18f43` for the Service App and data source.
3. Register the gRPC endpoint through the [Data Sources API](https://developer.webex.com/docs/api/v1/data-sources).
4. Select the Service App and data source in the CCAI configuration used by the **Virtual Agent Voice** activity.
