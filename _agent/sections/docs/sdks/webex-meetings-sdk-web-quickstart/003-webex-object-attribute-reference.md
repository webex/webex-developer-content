---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Object Attribute Reference
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-quickstart). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Meetings SDK. This guide is designed to provide developers with a concise walkthrough to swiftly set up, authorize, and test the core meeting functionalities within the Meeting SDK. 

---

By following the sequential flow of this document and integrating the provided code snippets, you'll be able to authenticate your application and create and manage your first meetings. Whether you're new to Webex's Meeting SDK or looking to brush up on the basics, this guide ensures a streamlined experience to get you up and running in no time. Let's dive in!

## Selected section

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
