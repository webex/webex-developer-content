---
type: Excerpt
canonical_url: https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Virtual Agent Call Summary API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary). [Full Markdown](../../../../docs/virtual-agent-transcripts-and-call-summary.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

This document describes how a custom widget in the WxCC agent desktop, or a third-party custom desktop, can interact with the Serving API service. This interaction allows the retrieval of Virtual Agent transcripts and the Virtual Agent transfer summary when a call is transferred from a virtual agent to a human agent.

## Selected section

## Virtual Agent Call Summary API

This is a unary gRPC API that returns the call summary of the conversation between the caller and the virtual agent (bot), based on the conversation ID. You can find the proto definition [here](https://s3.amazonaws.com/devportal.cms.devus1/serving_doc_2_0607f55ec1.proto).

1. Use the RPC, **InsightServing**.
    - **Input** - `InsightsServingRequest`
    - **Output** - `InsightsServingResponse`
2. Set `InsightType` to `CALL_INSIGHTS` (Enum value - 5). 

Here's an example request payload for retrieving the agent handoff summary:

```json
{
  "conversationId": "f4908103-82ef-405c-8f51-49f4de28181b",
  "insightType": 5,
  "messageId": "virtual-agent-call-summary",
  "orgId": "61194836-4001-42d3-bea8-56df1460e523"
}
```

And here's a sample response for the call summary:

```json
{
  "orgId": "org_01",
  "conversationId": "conversation_01",
  "roleId": "roleid_01",
  "utteranceId": "utterance_01",
  "role": "IVR",
  "insightType": "call_insights",
  "serviceProvider": "google",
  "startTimestamp": 1612862799876,
  "endTimestamp": 1612862799876,
  "publishTimestamp": 1612862799877,
  "isFinal": true,
  "messageId": "virtual-agent-call-summary",
  "configId": "configid_01",
  "languageCode": "en-US",
  "responseContent": {
    "content": "{\"hand_off_reason\":\"talk to an agent\",\"details\":\"The caller's reason for the call is to block their credit card. The call was handed off to a live human agent because the caller requested to talk to an agent.\",\"call_reason\":\"block credit card\"}",
    "callInsightType": "VA_CALL_SUMMARY"
  }
}
```
