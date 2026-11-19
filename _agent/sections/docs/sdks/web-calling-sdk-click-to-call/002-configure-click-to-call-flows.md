---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/web-calling-sdk-click-to-call
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Configure Click-to-Call Flows
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/web-calling-sdk-click-to-call). [Full Markdown](../../../../../docs/sdks/web-calling-sdk-click-to-call.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

Click-to-Call allows users to make calls without the need for a registered account and provides a convenient way for guests to join conversations and participate in audio calls. This article outlines how a click-to-call flow can be set up and utilized using the Web Calling SDK.

---

One of the key use cases is leveraging for **click-to-call** flows, where users can initiate a call by simply clicking a button or link. This is particularly useful in scenarios where the user does not need to manually enter any call details, making the process quick and user-friendly.

## Selected section

## Configure Click-to-Call Flows

There are a few steps involved in setting up the click-to-call flows using the SDK.



> **Info**
>
> This guide assumes that the application consumes the SDK via CDN. The code snippets and configuration within the steps vary if the application consumes the SDK via NPM. Refer to the [Quickstart Guide](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) for examples of these differences.



### 1. Set up the Configurations

Refer to the [Getting Started Documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) to understand how the `webexConfig` object is created.

Once you have your `webexConfig` object, set up your calling configuration:

```javascript
const callingClientConfig = {
   logger: loggerConfig,
   serviceData:{
      indicator: `guestcalling`,
      guestName: `guestName`
   },
   jwe: `<jwe_token_from_server>`,
};

const callingConfig = {
   clientConfig: clientConfig,
   callingClientConfig: callingClientConfig,
   logger: loggerConfig,
};
```



> **Info**
>
> Supports `guestcalling` indicator in `serviceData`, with optional `guestName` parameter for click-to-call flows.





> **Info**
>
> The difference between the `callingClientConfig` for a click-to-call flow and a regular calling flow is the presence of `jwe` and `guestcalling` as indicators within the `serviceData` argument for the click-to-call flows. In the case of a regular calling flow, this value is empty.



### 2. Set up the Calling Client

Create your `calling` object using the `webexConfig` and `callingConfig` objects:

```javascript
calling = await Calling.init({ webexConfig, callingConfig });
```

Register your `calling` object and extract the `callingClient` from the promise:

```javascript
calling.on("ready", () => {
   calling.register().then(async () => {
      callingClient = window.callingClient = calling.callingClient;
   });
});
```

Using the `callingClient` object, extract the `line` object from it and register the line :

```javascript
const line = Object.values(callingClient.getLines())[0];
line.on('registered', (lineInfo) => {
   // outbound call set-up will be placed here
});
line.register();
```

### 3. Set up the Outbound Call

Create the `call` instance for outbound calls using the `makeCall()` method of the `line` object:

```javascript
line.on('registered', (lineInfo) => {
   const call = line.makeCall();
});
```



> **Info**
>
> For a click-to-call flow, leave the parameter empty when calling `makeCall()`.



In order to utilize the `dial()` method, you need an audio stream object. To create this object use the `Calling` class:

```javascript
const localAudioStream = await Calling.createMicrophoneStream({ audio: true });
```

Trigger the `call` object's `dial()` method to initiate the call. Remember to pass the `localAudioStream` object as an argument:

```javascript
call.dial({ localAudioStream });
```



> **Info**
>
> To implement a click-to-call flow, run the above steps in a single sequence.



### 4. Deregister the Calling Client

After the call disconnects, it's a good practice to deregister the client:

```javascript
calling.deregister();
```
