---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Place a Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Place a Call

Starting an outgoing call to a designated destination involves a sequence of steps. First, you need to capture the microphone stream, since this step ensures your application is set to transmit voice. Once the microphone stream is in place, you'll need to create the `Call` object from the `Line`.

You can create a microphone stream in a couple of ways.

### Option 1

In this option, you'll use the `createMicrophoneStream()` within the `Calling` object to fetch the default microphone on the system. This option is only available when consuming the SDK via CDN.

```javascript
const localAudioStream = await Calling.createMicrophoneStream({ audio: true });

const call = line.makeCall({
  type: 'uri',
  address: 'destination'
});

await call.dial(localAudioStream);
```

### Option 2

This option is available to you if you consume the SDK via NPM. You'll need to use the `LocalMicrophoneStream` class from the SDK to create a microphone stream.

```javascript
import {LocalMicrophoneStream} from '@webex/calling';

const localStream = navigator.mediaDevices.getUserMedia({audio: true});
const audioTrack = localStream.getAudioTracks()[0];
const localMicStream = new LocalMicrophoneStream(new MediaStream([audioTrack])); 

const call = line.makeCall({
  type: 'uri',
  address: 'destination'
});

await call.dial(localMicStream);
```

As you navigate through the intricacies of initiating and managing calls, it's vital to note that the `Call` object is not just a static entity but a dynamic one, emitting various events during the course of a call. By actively listening for these events, developers can gain insights into the different transitions and states that a call might enter, be it `ringing`, `connected`, or `ended`. Monitoring these events allows for a more responsive and intuitive user experience, as your application can adjust in real-time based on the call's status. For instance, you might update the user interface to reflect when a call is on hold or when the other party has picked up. Incorporating this event-driven approach will ensure a robust and interactive calling experience for your users.

```javascript
call.on('progress', (correlationId) => {
  console.log('Call is ringing at the remote end');
});

call.on('connect', (correlationId) => {
  console.log('Call has been answered');
});

call.on('established', (correlationId) => {
  console.log('Call is now established. Media flows both ways');
});

call.on('disconnect', (correlationId) => {
  console.log('Call has been disconnected');
});

call.on('remote_media', (track) => {
  // Remote media information received from the SDK. This is relayed to the
  // application using the remote_media event
  document.getElementById('remote-audio').srcObject = new MediaStream([track]);
});
```

With the `Call` object ready, you can then utilize the `dial` method, incorporating the previously acquired microphone stream. This method combines the audio input with the call initiation, facilitating a communication link to your desired destination. This guide elucidates each step, providing you with a clear path to efficiently manage and initiate outgoing calls.

```javascript
await call.dial(localAudioStream);
```

Handling incoming calls requires a similar approach. The first step involves listening for the `incoming_call` event on the `Line`. This event signals the arrival of an incoming call and provides the initial alert to the application. Once this event is detected and an incoming call is acknowledged, the focus shifts to the `Call` object. Here, similar to outgoing calls, developers should actively listen to the set of events emitted by the `Call` object. These events provide real-time updates about the call's status, such as whether it's been answered, or disconnected. Once those listeners are ready, you can call the `answer` method to answer the call.

```javascript
let incomingCall;

line.on('line:incoming_call', (incomingCall) => {
  console.log('Incoming call arrived. Call information', incomingCall);
});

incomingCall.on('disconnect', (correlationId) => {
  console.log('Call has been disconnected');
});

incomingCall.on('remote_media', (track) => {
  // Remote media information received on the SDK. This is relayed to the
  // application using the remote_media event
  document.getElementById('remote-audio').srcObject = new MediaStream([track]);
});

incomingCall.answer();
```



> **Info**
>
> Client objects will be created based on the calling configuration inside a `Calling` instance.
