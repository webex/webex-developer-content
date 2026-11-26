---
type: Excerpt
canonical_url: https://developer.webex.com/docs/media-forking-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure the flow
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/media-forking-guide). [Full Markdown](../../../../docs/media-forking-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Implement, register, configure, and verify a partner-hosted Media Forking gRPC endpoint that receives caller and agent audio from Webex Contact Center.

## Selected section

## Configure the flow

1. Enable the test agent for Contact Center, assign its site, team, and desktop profile, and ensure the queue distributes calls to that team.
2. Open the target inbound flow in Flow Designer. Route the main flow through **Queue Contact** to the intended queue.
3. In **Event Flows**, connect **AgentAccepted** (called **AgentAnswered** in older flows) to **Start Media Stream**.
4. Under **Media streaming settings > Media destination**, select the authorized **Service App** directly.
5. Connect the activity's success and failure exits to **End Flow** so the event handler finishes.

   ![AgentAccepted connects to Start Media Stream, whose normal and failure paths both connect to End Flow.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd69fae50b7ceffa1/6aee21da421b3369aecc9439/agent-accepted-media-stream.jpg)

   *Example from a saved flow version. Generated activity labels can differ in your flow.*
6. Validate the flow, resolve validation errors, and publish it.
7. Map the test entry point to that flow and its published version label.

The activity needs an answered caller-agent conversation. A normal main path usually runs before the agent connects and can fail with `callNotAnswered`; use the agent-answer event handler for the inbound path above.

For queue-specific conditional logic in Flow Designer, see [Enabling media streaming for specific queues](https://help.webex.com/en-us/article/n5jhgdi/Enabling-media-streaming-for-specific-queues) in the Webex Help Center.
