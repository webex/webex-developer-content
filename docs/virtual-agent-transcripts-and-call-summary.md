---
type: Guide
title: Virtual Agent Transcripts and Call Summary
display_title: Virtual Agent Transcripts and Call Summary
canonical_url: https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/virtual-agent-transcripts-and-call-summary)

---

This document describes how a custom widget in the WxCC agent desktop, or a third-party custom desktop, can interact with the Serving API service. This interaction allows the retrieval of Virtual Agent transcripts and the Virtual Agent transfer summary when a call is transferred from a virtual agent to a human agent.

## Prerequisites

1. An access token with the `cjp:user` scope is required. See [Authentication](https://developer.webex.com/docs/authentication) for OAuth token generation.
2. The interaction ID of the current call is needed. For a custom widget in the WxCC Agent desktop, please refer [here](https://developer.webex.com/docs/desktop#javascript-sdk-and-modules). For third-party desktops, please refer [here](https://developer.webex.com/docs/contact-control-apis).

**Note:** The Interaction ID or Task ID is the same as the Conversation ID mentioned in this document.

## Server host details

To retrieve the server details:

1. Construct the following REST request:

    - `URL`: <https://u2c.wbx2.com/u2c/api/v1/user/catalog>
    - `Method`: GET
    - `Query Params`:

        | Parameter  | Value               |
        | ---------- | ------------------- |
        | `types`    | `WCC`               |
        | `services` | `wccai-serving-api` |

1. Add an `Authorization` header.

    **Example**: `Authorization: Bearer <access_token>`

1. Execute the REST request.

Here's an example response:

```json
{
  "services": [
     {
     "serviceName": "wccai-serving-api",
     "logicalNames": [
       "https://serving-api-streaming.wxcc-us1.cisco.com:443"
      ],
     "serviceUrls": [
        {
          "baseUrl": "https://serving-api-streaming.wxcc-us1.cisco.com:443",
          "priority": 5
        }
     ],
     "internalServiceUrls": [],
      "ttl": -1,
     "id": "urn:WCC:US1:wccai-serving-api"
   }
  ],
 "format": "servicelist"
}
 ```

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
