---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Call-Related Public APIs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Selected section

## Call-Related Public APIs

### getCall() Method

This method fetches a single `call` object that's active on a line. This API is implemented in the `line` object.

|                  |                            |
| ---------------- | -------------------------- |
| **Asynchronous** | No                         |
| **Parameters**   | CorrelationId of the call. |
| **Returns**      | Call Object(`ICall`)         |

```javascript
call = line.getCall(correlationId);
```

#### CallObject(ICall) Example

```javascript
{
    "callId": <string>,
    "callerInfo": {}
    "connected": boolean,
    "correlationId": <string>,
    "destination": {
        "type": 'uri',
        "address": 'tel:5954'
    },
    "deviceId": <string>,
    "direction": "outbound" | "inbound",
    "earlyMedia": boolean,
    "held": boolean,
    "mobiusUrl": "https://mobius.aintm-m-5.int.infra.webex.com/api/v1/calling/web/",
    "muted": boolean,
    "origin": {
        "type": "uri",
        "address": "sip:alice@example.com"
    },
}
```

### getConnectedCall() Method

Only a single call at a time can be in the connected state even if there are multiple calls active among multiple lines. The remaining calls will be on Hold. This API returns the `call` object which is in the `connected` state. This API is provided by the `CallingClient` object since the information on which line has a call in the connected state is unknown.

|                  |                        |
| ---------------- | ---------------------- |
| **Asynchronous** | No                     |
| **Parameters**   | No parameters required |
| **Returns**      | Call Object(`ICall`)     |

```javascript
call = callingClient.getConnectedCall(correlationId);
```

### getActiveCalls() Method

A line has the ability to support multiple calls at the same time. In order to fetch all the calls that are active across all lines, this API can be used. It returns a key-value pair where the key is the `lineId(deviceId)` and its value is an array of `call` objects on that line. This API is provided by the `CallingClient` object.

|                  |                        |
| ---------------- | ---------------------- |
| **Asynchronous** | No                     |
| **Parameters**   | No parameters required |
| **Returns**      | `LineToCallMap` object   |

```javascript
calls = callingClient.getActiveCalls();
```

Example key-value pair returned by the `getActiveCalls()` method:

#### LineToCallMap Example

```json
{
    "ca3a511e-81b4-3155-ab47-ff7bd8c0c189": [
     {
         callId: "ce8badee-04cc-463f-a5cf-738b51157165",
         callerInfo: {}
         connected: true,
         correlationId: "0fa25099-01f0-44bc-b988-230c6ba2d25f",
         destination: {
             type: 'uri',
             address: 'tel:5954'
         },
         deviceId: "ca3a511e-81b4-3155-ab47-ff7bd8c0c189",
         direction: "outbound",
         earlyMedia: false,
         held: true,
         mobiusUrl: "https://mobius.aintm-m-5.int.infra.webex.com/api/v1/calling/web/",
         muted: false,
         origin: {
             type: "uri",
             address: "sip:alice@example.com"
         },
     },
     {
         callId: "ce8badee-04cc-463f-a5cf-738b51157165",
         callerInfo: {}
         connected: false,
         correlationId: "0fa25099-01f0-44bc-b988-230c6ba2d25f",
         destination: {
             type: 'uri',
             address: 'tel:5954'
         },
         deviceId: "ca3a511e-81b4-3155-ab47-ff7bd8c0c189",
         direction: "inbound",
         earlyMedia: false,
         held: false,
         mobiusUrl: "https://mobius.aintm-m-5.int.infra.webex.com/api/v1/calling/web/",
         muted: false,
         origin: {
             type: "uri",
             address: "sip:alice@example.com"
         },
     },],
    "a1cff23f-b3b6-323c-b213-5e12371cfbd6": [
     {
         callId: "b951015c-4a93-428e-9c33-91d894807877",
         callerInfo: {}
         connected: true,
         correlationId: "e16dac14-64dc-4317-8be5-8bc807da44eb",
         destination: {
             type: 'uri',
             address: 'tel:5009'
         },
         deviceId: "a1cff23f-b3b6-323c-b213-5e12371cfbd6",
         direction: "outbound",
         earlyMedia: false,
         held: false,
         mobiusUrl: "https://mobius.aintm-m-5.int.infra.webex.com/api/v1/calling/web/",
         muted: false,
         origin: {
             type: "uri",
             address: "sip:alice@example.com"
         },
    },],
}    
```
