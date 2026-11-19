---
type: Excerpt
canonical_url: https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Virtual Agent transcripts API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary). [Full Markdown](../../../../docs/virtual-agent-transcripts-and-call-summary.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

---

This document describes how a custom widget in the WxCC agent desktop, or a third-party custom desktop, can interact with the Serving API service. This interaction allows the retrieval of Virtual Agent transcripts and the Virtual Agent transfer summary when a call is transferred from a virtual agent to a human agent.

## Selected section

## Virtual Agent transcripts API

This is a server-side gRPC streaming API that takes flags and a conversation ID as input. It returns the transcripts of the conversation between the caller and the virtual agent (Bot) in a historical manner. You can find the proto definitions [here](https://github.com/CiscoDevNet/webex-contact-center-ai-sample-code/blob/main/serving-api/protobuf/com/cisco/wcc/ccai/v1/serving.proto).

1. Use the RPC, **StreamingInsightServing**.
    - **Input**- `StreamingInsightServingRequest`
    - **Output** - `stream StreamingInsightServingResponse`

    Here's an example `StreamingInsightServingRequest` request payload for retrieving the VA and caller transcripts:

    ```json
        {
            "insightServingRequest": {
            "agentDetails": {
              "agentId": "1234"
            },
            "conversationId": "4801c6ce-7a58-4704-b674-1748d53b7085",
            "orgId": "61194836-4001-42d3-bea8-56df1460e522",
            "historicalVirtualAgent": true,
            "historicalTranscripts": true
        }
    ```

1. The response will be an array of transcripts, including both the speech transcripts of the virtual agent and the caller.

Here's a sample response object for the Virtual Agent transcript:

```json
{
  "orgId": "orgid_01",
  "conversationId": "conversation_01",
  "roleId": "roleid_02",
  "utteranceId": "utterance_04",
  "role": "IVR",
  "insightType": "virtual_agent",
  "serviceProvider": "nuance",
  "startTimestamp": 1612868857983,
  "endTimestamp": 1612868857983,
  "publishTimestamp": 1612868857983,
  "isFinal": true,
  "messageId": "messageId_01",
  "configId": "Test123",
  "languageCode": "en-US",
  "responseContent": {
     "replyText": [
      "Your flight from Bangalore to Delhi on August 31st for 85 people is booked. Thank you!"
    ],
     "agentTransfer": {
     "metadata": {
        "userData": {
           "timezone": "Asia/Kolkata"
         }
       }
     }
   }
}
```

And here's a sample response object for the Caller transcript

```json
{
  "orgId": "org_01",
  "conversationId": "conversation_01",
  "roleId": "roleid_01",
  "utteranceId": "utterance_01",
  "role": "IVR",
  "insightType": "transcript",
  "serviceProvider": "google",
  "startTimestamp": 1612862799876,
  "endTimestamp": 1612862799876,
  "publishTimestamp": 1612862799877,
  "isFinal": true,
  "messageId": "mesage_id_01",
  "configId": "configid_01",
  "languageCode": "en-US",
  "responseContent": {
    "alternatives": [
      {
        "transcript": "I would like to book a flight to New york city."
      }
    ],
    "result_end_time": {
      "nanos": 360000000
    },
    "messageType": "TRANSCRIPT"
  }
}
```
