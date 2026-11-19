---
type: Guide
title: Web Meetings SDK | Quickstart Guide
display_title: Quickstart
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart)

Welcome to the Quick Start Guide for the Webex Meetings SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core meeting functionalities within the Meeting SDK. 

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and create and manage your first meetings. Whether you're new to Webex's Meeting SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Import the Meetings SDK

To install the latest stable version of the Meetings SDK use either NPM or CDN.

### NPM



> **Info**
>
> We test against the [Active LTS](https://github.com/nodejs/Release#release-schedule) (Long Term Support) version of Node.js and use `npm@6` to run [security audits](https://docs.npmjs.com/getting-started/running-a-security-audit).



The Meetings SDK is available as a `nodejs` module via NPM. You can install it using either `yarn` or `npm` utilities:

```bash
 yarn add webex
```

or

```bash
npm install webex
```

### CDN

A minified version of the Meeting SDK is also provided via the [unpkg](https://unpkg.com/) or [jsdelivr](https://jsdelivr.com/) Content Delivery Networks (CDN). To include the CDN Meeting SDK:

```html
 <!-- unpkg -->
 <script crossorigin src="https://unpkg.com/webex/umd/webex.min.js"></script>
 <!-- jsdelivr -->
 <script crossorigin src="https://cdn.jsdelivr.net/npm/webex/umd/webex.min.js"></script>
```

If you're already using a bundler like [Webpack](https://webpack.js.org/) or [Rollup](https://rollupjs.org/)) you can simply import or require the package and use the above snippet, assigning the initialized `webex` variable to `window.webex`.

We also provide a `meetings` specific SDK via [unpkg](https://unpkg.com/). Access by including the following code:

```html
 <script crossorigin src="https://unpkg.com/webex/umd/meetings.min.js"></script>
```

## Initialize the SDK

If you don't already have a Cisco Webex account, visit the [Webex Developer Portal](https://developer.webex.com/) to create your account and retrieve your **access token** from the following page: [Getting and Using your Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token).

To create a new `Webex` object, replace `<AUTHORIZATION/BOT TOKEN>` below with your Personal Access Token from the Developer Portal:

```js
const Webex = import(`webex`);
const webex = Webex.init({
  credentials: {
    access_token: `<AUTHORIZATION/BOT TOKEN>`
  }
});
```

You can only create rooms or meetings once the `Webex` object is ready. You'll want to attach a listener for the `Webex` object's `ready` event and proceed only after that event has fired. Here's a complete workflow:

1. Listen for the ready event and log a message.
1. Create a room titled "My First Room".
1. Add Alice and then Bob to the new room.
1. Send a "Hi Everyone" message to all the participants in the room.

```js
// Listen for the ready event
webex.once('ready', () => {
    console.log('Authentication#initWebex() :: Webex Ready');
  });

webex.rooms.create({ title: `My First Room` }).then(room => {
  return Promise.all([
    webex.memberships.create({
      roomId: room.id,
      personEmail: `alice@example.com`
    }),
    webex.memberships.create({
      roomId: room.id,
      personEmail: `bob@example.com`
    })
  ]).then(() =>
    webex.messages.create({
      markdown: `**Hi Everyone**`,
      roomId: room.id
    })
  );
});
```

## Webex Object Attribute Reference

The following tables cover all of the available configuration attributes for the `webex` object.

### Default Attributes



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** |
| --- | --- | --- | --- | --- |
| 1.  | `credentials` | Use this object to set up credentials for authentication. | **Object** | Yes |
| 1.a | `access_token` | Access token used to communicate with Webex. | **String** | No |
| 1.b | `clientType` | Type of client communicating with Webex, an example would be "Web". | **String** | Yes |
| 2.  | `device` | Use this object to set the settings for the device created in Webex. | **Object** | Yes |
| 2.a | `validateDomains` | Validate domains against the allowed domains. | **Boolean** | Yes |
| 2.b | `allowedDomains` | The allowed domains to validate domains against. | **String[]** | No |
| 2.c | `ephemeral` | Enable or disable "ephemeral" mode which sets a TTL of 30 minutes on the registration of the device created in Webex. | **Boolean** | Yes |
| 3.  | `storage` | Use this object to set storage properties for the `webex` object. | **Object** | Yes |
| 3.a | `boundedAdapter` | Used to store information pertaining to the `webex` object. | **StorageAdapterLocalStorage** | Yes |
| 3.b | `unboundedAdapter` | Used to store information outside the scope of the `webex` object. | **LocalForageStoreAdapter** | Yes |

### Credentials



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** |
| --- | --- | --- | --- | --- |
| 1. | `access_token` | Access token used to communicate with Webex. | **String** | No |
| 2. | `clientType` | Type of client communicating with Webex, an example would be "Web". | **String** | Yes |
| 3. | `client_id` | Unique client ID assigned to the developer for Oauth 2.0. | **String** | No |
| 4. | `client_secret` | Unique client secret assigned to the developer for Oauth 2.0. | **String** | No |
| 5. | `scope` | [Scopes](https://developer.webex.com/docs/integrations#scopes) define the privilege level of the access token. They determine what the client can and cannot do. | **String** | No |
| 6. | `redirect_uri` | Redirect URI points to the landing page of the developer's application after successful authentication. | **String** | No |

### Storage



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** |
| --- | --- | --- | --- | --- |
| 1. | `boundedAdapter` | Used to store information pertaining to the `webex` object. | **StorageAdapterLocalStorage** | Yes |
| 2. | `unboundedAdapter` | Used to store information outside the scope of the `webex` object. | **LocalForageStoreAdapter** | Yes |

### Meetings



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** |
| --- | --- | --- | --- | --- |
| 1. | `mediaSettings` | Use this object to set media settings for meetings. | **Object** | No |
| 1.a | `pstn` | Enable or disable a PSTN connection within the meeting. | **Boolean** | No |
| 2. | `reconnection` | Use this object to set reconnection settings for a meeting. | **Object** | No |
| 2.a | `enabled` | Enable or disable reconnection to a meeting. | **Boolean** | No |
| 2.b | `autoRejoin` | Enable or disable automatic rejoin once a connection is restored. | **Boolean** | No |
| 3. | `logging` | Use this object to set logging. | **Object** | No |
| 3.a | `enable` | Enable or disable logging. | **Boolean** | No |
| 3.b | `verboseEvents` | Enable or disable verbose level debugs. | **Boolean** | No |
| 4. | `resolution` | Object to the resolution of the video. | **Object** | No |
| 4.a | `maxWidth` | Maximum width of the video. | **Int** | No |
| 4.b | `maxHeight` | Maximum height of the video. | **Int** | No |
| 4.c | `idealWidth` | Ideal width of the video. | **Int** | No |
| 4.d | `idealHeight` | Ideal height of the video. | **Int** | No |
| 5. | `screenResolution` | Object to set resolution of screen share. | **Object** | No |
| 5.a | `maxWidth` | Maximum width of the screenshare video. | **Int** | No |
| 5.b | `maxHeight` |  Maximum height of the screenshare video. | **Int** | No |
| 5.c | `idealWidth` | Ideal width of the screenshare video. | **Int** | No |
| 5.d | `idealHeight` | Ideal height of the screenshare video. | **Int** | No |
| 6. | `bandwidth` | Object to set bandwidth constraints for a meeting. | **Object** | No |
| 6.a | `audio` | Maximum bandwidth value for audio. | **Int** | No |
| 6.b | `video` | Maximum bandwidth value for video, independent of resolution. | **Int** | No |
| 6.c | `startBitrate` | Sets the starting bitrate for the media connection. | **Int** | No |
| 7. | `videoShareFrameRate` | Sets the frame rate of the screenshare. | **Int** | No |
| 8. | `aspectRatio` | Sets the aspect ratio of the video. | **Float** | No |
| 9. | `autoUploadLogs` | When enabled, as calls are ended, SDK logs are uploaded and correlated. | **Boolean** | No |
| 10. | `enableRtx` | Enable or disable RTP packet retransmission. | **Boolean** | No |
| 11. | `receiveTranscription` | Enable receipt of transcription from Webex meeting services. | **Boolean** | No |
| 12. | `enableExtMap` | Enable or disable the advertising of RTP extension mapping within the SDP during WebRTC negotiation. | **Boolean** | No |
| 13. | `experimental` | Object to turn expermiental features on or off. | **Object** | No |
| 13.a | `enableMediaNegotiatedEvent` | Enable or disable emission of event from `meeting` object when media is negotiated successfully. | **Boolean** | No |
| 13.b | `enableUnifiedMeetings` | Enable or disable the improved meeting experience associated with a space. Refer to this [help article](https://help.webex.com/en-us/article/gxw5jz/Webex-App-%7C-Improved-meetings-associated-with-a-space) for more details. | **Boolean** | No |
| 13.c | `enableAdhocMeetings` | Enable or disable the creation of an instant meeting. | **Boolean** | No |
| 14. | `degradationPreferences` | Object to set behavior of meetings when experiencing degradation. | **Object** | No |
| 14.a | `maxMacroblocksLimit` | Set the maximum number of blocks that can be requested by the web application during a meeting. Defaults to 8192. | **Int** | No |

### Other Attributes



| **S.no** | **Attribute** | **Description** | **Data Type** | **Default Attribute?** |
| --- | --- | --- | --- | --- |
| 1. | `appPlatform` | Platform or name of the application consuming the Webex Web Meetings SDK. | **String** | No |
| 2. | `appVersion` | Version of the application consuming the Webex Web Meetings SDK. | **String** | No |
| 3. | `fedRamp` | Set this flag to true if you are operating in the FedRAMP environment. | **Boolean** | No |
| 4. | `appName` | Name of the application consuming the Webex Web Meetings SDK. | **String** | No |

Here's a complete example `Webex` object:

```js
{
  appPlatform: 'testClient',
  fedRamp: true,
  credentials: {
    access_token: 'your_webex_access_token',
    clientType: 'confidential',
    client_id: 'id',
    client_secret: 'secret',
    scope: 'spark:all spark:kms',
    redirect_uri,
  },
  logger: {
    level: 'debug',
    historyLength: 1000,
  },
  appName: 'sdk-samples',
  storage: {
    boundedAdapter: new StorageAdapterLocalStorage('webex'),
    unboundedAdapter: new LocalForageStoreAdapter('web-client-internal'),
  },
  meetings: {
    mediaSettings: {
      pstn: false,
    },
    reconnection: {
      enabled: false,
      autoRejoin: true,
    },
    metrics: {
      clientName: 'WEBEX_JS_SDK',
      clientType: 'WEBEX_SDK',
    },
    logging: {
      enable: true,
      verboseEvents: true,
    },
    resolution: {
      maxWidth: 1280,
      maxHeight: 720,
      idealWidth: 1280,
      idealHeight: 720,
    },
    screenResolution: {
      maxWidth: 1920,
      maxHeight: 1080,
      idealWidth: 1920,
      idealHeight: 1080,
    },
    bandwidth: {
      audio: 64000,
      video: 4000000,
      startBitrate: 2000,
    },
    videoShareFrameRate: 30,
    aspectRatio: 1.7695852534562213,
    autoUploadLogs: true,
    enableRtx: true,
    receiveTranscription: false,
    enableExtmap: false,
    experimental: {
      enableMediaNegotiatedEvent: false,
      enableUnifiedMeetings: false,
      enableAdhocMeetings: false,
      enableTurnDiscovery: true,
    },
  },
};
```

## Use a Proxy Agent to Open a WebSocket Connection

For consumers who are not using the SDK via the browser, it may be necessary to configure a proxy agent to connect with Mercury and open a WebSocket in a proxy environment. This can be done by configuring an agent as part of a `DefaultMercuryOptions` config object. The agent object will then be injected into the SDK and used in the Mercury plug-in during WebSocket construction as an option property, allowing a connection to be established via the specified proxy URL:

```js
const webex = require(`webex`);
const HttpsProxyAgent = require('https-proxy-agent');

let httpsProxyAgent = new HttpsProxyAgent(url.parse(proxyUrl));

webex.init({
  config: {
    defaultMercuryOptions: {
      agent: httpsProxyAgent
    }
  }
});
```
