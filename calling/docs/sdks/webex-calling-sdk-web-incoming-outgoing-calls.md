---
type: Guide
title: Web Calling SDK | Incoming and Outgoing Calls
display_title: Calls
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-incoming-outgoing-calls)

The `CallingClient` module in the Calling SDK provides inbound and outbound call functionality on registered lines.

---

A call instance is created for every call and then used to dial the call and listen for events. This document covers how the call instance is obtained and used in inbound/outbound calls.

## Call Object

After the lines have been registered, you can utilize call functionality on any of these registered lines. To initiate a call, you can use the `makeCall()` method when invoked on a specific line. When an inbound call is received by the client from Webex Calling, the Calling SDK dispatches an event, and within the event payload, a call instance is returned.

This call instance, provided by the Calling SDK, is of type `ICall`. It provides a range of methods that enable you to perform specific actions and manage the call as it progresses through various states.

### Call Methods

| **Method** | **Description** | **Returns** | **Visibility** |
| --- | --- | --- | --- |
| `answer` | Accepts or answers an incoming call from Webex Calling. | `void` | Public |
| `dial` | Dials the outgoing call to the destination. | `void` | Public |
| `end` | Ends an ongoing call. | `void` | Public |
| `sendDigit` | Sends a DTMF digit on an established call. | `void` | Public |
| `mute` | Mutes the local stream of this call instance. | `void` | Public |
| `doHoldResume` | Places the remote end of this call on either hold/resume on the current state of the call. | `void` | Public |
| `completeTransfer` | Initiates a transfer towards a target. | `void` | Public |
| `updateMedia` | Updates the microphone stream used during the call. | `void` | Public |

### Call Events

| **Event** | **Description** | **Payload** |
| --- | --- | --- |
| `incoming_call` | Incoming call is received. | Call Object (`ICall`) |
| `caller_id` | Remote end calling information determined. | `CallId` |
| `progress` | Remote end is ringing or has provided a cut-through. | `CorrelationId(string)` |
| `connect` | The remote end has answered the call. | `CorrelationId(string)` |
| `established` | Two-way media has now been established. | `CorrelationId(string)` |
| `remote_media` | Remote media track received. Use this to play out remote media on client. | Track object (`MediaStreamTrack`) |
| `disconnect` | Remote end has disconnected the call. | `CorrelationId(string)` |
| `held` | Remote end has been put on hold successfully. | `CorrelationId(string)` |
| `resumed` | Remote end has been put on hold successfully. | `CorrelationId(string)` |
| `call_error` | An error has occurred in the call | Error object. `(CallError)` |
| `hold_error` | An error has occurred while placing call on hold. | Error object (`CallError`) |
| `resume_error` | An error has occurred while placing call on resume. | Error object (`CallError`) |
| `transfer_error` | An error has occurred while transferring the call. | Error object (`CallError`) |

## Inbound Calls

In order to receive incoming calls, listen for the `incoming_call` event on the `line` object.

```javascript
line.on('line:incoming_call', (call: ICall) => {
  //  Call object received. Store this object and listen for events on the call
});
```

Once the call is received by the application, you can use the `answer()` method to answer the call. This method requires a `localAudioStream` as an argument.

```javascript
call.answer({ localAudioStream });
```

Once the call is answered from the application side, listen for additional events received on the `call` instance such as `remote_media`, `disconnect`, `caller_id` `update`, etc. More details on those events can be found in the Call Events table above.


```javascript
call.on('remote_media', (track: MediaStreamTrack) => {
  // store remote audio received and use it to open media channel 2-way
});
```

## Outbound Calls

Create the `call` instance first for outbound calls using the `makeCall()` method of the `line` object.

```javascript
call = line.makeCall();
```

Trigger the `call` object's `dial()` method to initiate the call. This method requires a `localAudioStream` as an argument.

```javascript
call.dial({ localAudioStream });
```

Listen for events on the `call` object to track the further progress of the call and establish 2-way audio.

```javascript
call.on('progress', (correlationId: string) => {
  // Process call progress, this event indicates that the call is ringing on the called party side
});
```

```javascript
call.on('connect', (correlationId: string) => {
  // Process connect event, this is received when the call has been answered from the called party side
});
```

```javascript
call.on('remote_media', (track: MediaStreamTrack) => {
  // Add code to store remote audio received and use it to open media channel 2-way
});
```

## Call Disconnect

Disconnect the call using the `call` object's `end()` method or listen for `disconnect` events coming from the other side.

Refer to the below examples:

1.  Listen for a `disconnect` event if the remote party disconnects the call.

    ```javascript
    call.on('disconnect', (correlationId: string) => {
      // Add action to clear out the call on the application
    });
    ```

2.  Once the disconnect event is received use the `call` object's `end()` method available to disconnect the call.

    ```javascript
    call.end();
    ```

## Error Handling

Calls will occasionally experience errors. An error event is triggered by the `call` object when an error is encountered. Listen for the `call_error` event to handle error scenarios.


```javascript
call.on('call_error', (callError: CallError) => {
  // Handle the error received for the ongoing call
    console.log('Error encountered on call with Id and description', 
      callError.getCallError().correlationId, callError.getCallError().message);
});
```

The `CallError` object contains the following members:

- `message` - Description of the call error.
- `type` - Type of error. This error can be either a call control error or a media error.
- `correlationId` - Correlation ID of the call that faced the issue.

## Updating Media

While a call is in progress, it's possible to update media to allow a developer to switch from one device to another. In order to do that, the `call` object provides an `updateMedia()` method.

First, create a `constraints` object using the new device ID and then pass that `constraints` object to the `Calling` object's `createMicrophoneStream()` method, creating a new `Stream` object.

### CDN

```javascript
const constraints = {
  audio: true,
  deviceId: 'DEVICE_ID'
};

const newStream = await Calling.createMicrophoneStream(constraints);
```

### NPM

```javascript
import {LocalMicrophoneStream} from '@webex/calling';

const constraints = {
  audio: true,
  deviceId: 'DEVICE_ID'
};

const localStream = navigator.mediaDevices.getUserMedia(constraints);
const audioTrack = localStream.getAudioTracks()[0];
const newStream = new LocalMicrophoneStream(new MediaStream([audioTrack])); 
```

Then, pass the `Stream` object to the `call` object's `updateMedia()` method.

```javascript
call.updateMedia(newStream);
```

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
