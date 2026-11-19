---
type: Guide
title: Web Calling SDK | Quickstart Guide
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart)

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Install the Calling SDK

To install and consume the latest stable version of the Calling SDK you can use NPM or CDN.

### NPM



> **Info**
>
> We test against the [Active LTS](https://github.com/nodejs/Release#release-schedule) (Long Term Support) version of Node.js and use `npm@6` to run [security audits](https://docs.npmjs.com/getting-started/running-a-security-audit).



The Calling SDK is available in two forms as a `nodejs` module via NPM.
Install either of the following modules based on how you'd like to consume the Calling SDK. For more information on the ways to consume the module, refer to the section below.

* [@webex/calling](https://www.npmjs.com/package/@webex/calling)
* [webex](https://www.npmjs.com/package/webex)

When using the `@webex/calling` package, use these commands to install the package. You'll use these packages for "Option 1" in the section below.
```bash
npm install --save @webex/calling
```
or
```bash
yarn add @webex/calling
```

When using the `webex` package, use these commands to install the package. You'll use this for "Option 2" in the section below.
```bash
npm install --save webex
```
or 
```bash
yarn add webex
```

### CDN

A minified version of the Calling SDK is also provided via the `unpkg.com` Content Delivery Network (CDN). To include the CDN Calling SDK:

```javascript
<script src='https://unpkg.com/webex/umd/calling.min.js'></script>
```

## Initialize the Calling SDK

To initialize the Calling SDK, you can use either a Webex object or Webex configuration. The initialization of the SDK also depends on how it is being consumed in the application. The process varies between the CDN and NPM forms of consumption.

### Option 1

This option includes different steps based how you consume the SDK in your application. Use this option when you've already initialized a `webex` object prior to initializing the Calling SDK. This option requires you to have installed the `@webex/calling` package.

#### CDN

1. Initialize a Webex object with an access token and required configuration. Refer to the [Quickstart guide](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart) on how to initialize the `webex` object. You can also refer to the `webexConfig` object in Option 2 as a reference.
2. [Register with Webex Device Manager (WDM) and establish a mercury connection](https://webex.github.io/webex-js-sdk/api/#register).
3. Pass the `webex` and `callingConfig` objects as arguments and create a new `Calling` instance which initializes the different client modules. (Refer to the table in the [Calling Configuration](#calling-configuration) section to identify Calling Configuration attributes).

```javascript
const calling = await Calling.init({ webex, callingConfig });
```

#### NPM

1. Initialize a Webex object with an access token and required configuration. Refer to the [Quickstart guide](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart) on how to initialize the `webex` object. You can also refer to the `webexConfig` object in Option 2 as a reference.
2. [Register with Webex Device Manager (WDM) and establish a mercury connection](https://webex.github.io/webex-js-sdk/api/#register).
3. Pass the `webex` and `CallingClientConfig` as arguments and create a new `CallingClient` instance.

```javascript
import {createClient} from '@webex/calling';

const callingClientConfig = {
  logger: {
    level: 'info'
  },
  serviceData: { // This configuration is optional for Webex Calling. It is mandatory for Webex Contact Center
    indicator: 'contactcenter',
    domain: 'rtw.prod-us1.rtmsprod.net'
  },
};

const callingClient = await createClient(webex, callingClientConfig);
```

Similarly, initialize other client modules available in the Calling SDK to utilize features like voicemail and contacts.

```javascript
import {createVoicemailClient, createContactsClient, createCallHistoryClient, createCallSettingsClient} from '@webex/calling';

const config = {
  logger: {
    level: 'info'
  },
};

const vmClient = await createVoicemailClient(webex, config);
const contactClient = await createContactsClient(webex, config);
const callHistoryClient = await createCallHistoryClient(webex, config);
const callSettingsClient = await createCallSettingsClient(webex, config);
```

### Option 2

Use this option when you have not initialized the `webex` object prior to initializing the Calling SDK. This option requires you to have installed the `webex` package. The steps are common for both NPM and CDN methods. Note the first line of the code snippet, which should be avoided while using CDN.

1. Pass the `webexConfig` and `callingConfig` objects as arguments and create a new `Calling` instance. (Refer to the [attribute section](https://github.com/webex/webex-js-sdk/wiki/Quickstart-Guide#default-attributes) for Webex configuration attributes).
2. Wait for the Calling instance to be ready by listening for the `ready` event.
3. Once the `ready` event is received, call the `register()` method to trigger Webex Device Manager registration, which establishes a mercury connection and initializes the various client modules within Calling object.

```javascript
import Calling from 'webex/calling'; // NPM only

// Create the Webex configuration

const webexConfig = {
  config: {
    logger: {
      level: 'debug' // Set the desired log level
    },
    meetings: {
      reconnection: {
        enabled: true
      },
      enableRtx: true
    },
    encryption: {
      kmsInitialTimeout: 8000,
      kmsMaxTimeout: 40000,
      batcherMaxCalls: 30,
      caroots: null
    },
    dss: {}
  },
  credentials: {
    access_token: 'access_token'
  }
};

// Create the calling configuration

const callingConfig = {
  clientConfig: {
    calling: true,
    contact: true,
    callHistory: true,
    callSettings: true,
    voicemail: true
  },
  callingClientConfig: {
    logger: {
      level: 'info'
    }
  },
  logger: {
    level: 'info'
  }
};

// Create the Calling object

const calling = await Calling.init({ webexConfig, callingConfig });
let callingClient;
calling.on('ready', () => {
  calling.register().then(() => {
    callingClient = calling.callingClient;
  });
});
```

## Authorize with Webex Calling

Initiating the authorization process with Webex Calling is the first step to harness the communication capabilities of the SDK. Before diving into call operations, you must first obtain the `Line` object from the `CallingClient`. Once you have the `Line` object in hand, you can invoke the `line.register()` function to create a device, laying the groundwork for initiating and managing voice calls. Before triggering the `register()` method, however, it's crucial to listen for the `registered` event to ensure the device is successfully registered and ready for operations. This section will guide you through these steps.

```javascript
// Get Line object from the callingClient. Currently, only a single
// line is supported in the Calling package

const line = Object.values(callingClient.getLines())[0];

// Listen for the registered event from the line

line.on('registered', (lineInfo) => {
  console.log('Line information: ', lineInfo);
});

line.register();
```

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



## Calling Configuration Details

This is the definition for a `callingConfig` object:

```javascript
callingConfig: {
 clientConfig: {
  calling: boolean,
  contact: boolean,
  callHistory: boolean,
  callSettings: boolean,
  voicemail: boolean,
 },
 callingClientConfig: {
  logger: {
   level: string
  },
  discovery: {
   country: string,
   region: string,
  },
  serviceData: {
   domain: string,
   indicator: string,
   guestName: string
  }
 },
 logger: {
  level: string
 }
}
```

The following tables cover the different configuration attributes present inside the `callingConfig` object.

### Client Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `calling` | Toggles the availability of the `callingClient` module.  | `Boolean` | No | Yes |
| 2. | `contact` | Toggles the availability of the `contactClient` module. | `Boolean` | No | Yes |
| 3. | `callHistory` | Toggles the availability of the `callHistory` module. | `Boolean` | No | Yes |
| 4. | `callSettings` | Toggles the availability of the `callSettings` module. | `Boolean` | No | Yes |
| 5. | `voicemail` | Toggles the availability of the `voicemailClient` module. | `Boolean` | No | Yes |

### Calling Client Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `discovery` |  | `Object` | No | Yes |
| 1.a. | `country` | Country from where the device registration is triggered. It has to be an Alpha-2 code as per ISO 3166-1 standards. Here's the list of [officially assigned Alpha-2 codes from Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements). | `String` | No | Yes |
| 1.b. | `region` | Region from where the device registration is triggered. It should be one of the following: `AP-SOUTHEAST`, `US-EAST`, `EU`, or `EU-CENTRAL`. | `String` | No | Yes |
| 2. | `serviceData` |  it represents the service data of the SDK. | `String` | No | Yes |
| 2.a. | `domain` | Identifies which service is using the Calling SDK. | `String` | Yes | Yes |
| 2.b. | `indicator` | The type of service being used in the SDK. Its value should be `CALLING`, `CONTACT_CENTER`, or `GUEST_CALLING`. | `ServiceIndicator` | No | No |
| 2.c. | `guestName` | The `guestName` attribute is used in the SDK to indicate the name of the guest within a calling service. | `String` | No | Yes |
| 3.  | `logger` | Logger configuration. | `Object` |  |  |

### Logger Configuration



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** | **Public Attribute?** |
| --- | --- | --- | --- | --- | --- |
| 1. | `level` | Maximum log level that should be printed to the console. Possible values:`silent`, `error`, `warn`, `log`, `info`, `debug`, `trace` | `String` |  | Yes |
