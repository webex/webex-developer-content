---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Initialize the Calling SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Calling SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core calling functionalities within the Calling SDK.

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and initiate your first calls. Whether you're new to Webex's Calling SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

## Initialize the Calling SDK

To initialize the Calling SDK, you can use either a Webex object or Webex configuration. The initialization of the SDK also depends on how it is being consumed in the application. The process varies between the CDN and NPM forms of consumption.

### Option 1

This option includes different steps based how you consume the SDK in your application. Use this option when you've already initialized a `webex` object prior to initializing the Calling SDK. This option requires you to have installed the `@webex/calling` package.

#### CDN

1. Initialize a Webex object with an access token and required configuration. Refer to the [Quickstart guide](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart) on how to initialize the `webex` object. You can also refer to the `webexConfig` object in Option 2 as a reference.
2. [Register with Webex Device Manager (WDM) and establish a mercury connection](https://webex.github.io/webex-js-sdk/api/#register).
3. Pass the `webex` and `callingConfig` objects as arguments and create a new `Calling` instance which initializes the different client modules. (Refer to the table in the [Calling Configuration](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart#calling-configuration) section to identify Calling Configuration attributes).

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
