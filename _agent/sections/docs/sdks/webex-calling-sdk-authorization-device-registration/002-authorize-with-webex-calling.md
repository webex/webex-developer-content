---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Authorize with Webex Calling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## Authorize with Webex Calling

Registering an endpoint with Webex Calling is a pivotal step in authorizing a user to access voice and video communication features. Once a user is provisioned in an organization licensed for Webex Calling, the `CallingClient` module can be used to initiate the registration process. That involves obtaining an access token via OAuth 2.0 authentication. Upon successful authentication, the `CallingClient` module registers the endpoint, thereby enabling it to place and receive calls through the Webex cloud. Once registration is complete, the SDK automatically sends requests at regular intervals to maintain the endpoint's active registration status.

Additional details regarding the registration process can be found below.

### Obtaining a Line Object

A line object is created at the time of the `callingClient` initialization itself. It can be obtained by fetching the list of all the lines using `getLines` method in the callingClient module. However, the SDK only supports a single line at the moment.

For example:

```js
const callingClient  = calling.callingClient;
const lines = callingClient.getLines();
```

The constant, `lines`, is an object where the keys are the `lineId` of each line and the values are the line Objects themselves.



> **Info**
>
> Please refer to [the getting started documentation](https://developer.webex.com/docs/sdks/webex-calling-sdk-web-quickstart) for information on the creation and initialization of the `Calling` object. The example above is just pseudocode indicating that `callingClient` is a part of the main `calling` object).



Each of the line objects contain the following information:



|**Properties**|**Description**|**Type**|
| --- | --- | --- |
| `lineId` | Unique ID provisioned per line in order to distinguish and identify them within the application. |`string<uuid>` |
| `mobiusDeviceId` | Unique ID provisioned per line for communication between the SDK and the backend. |`string<uuid>` |
| `phoneNumber` | External phone number for the line. | `string` |
| `extension` |  Internal extension for the line. | `string` |
| `status` | Registration status of the line (initially set to inactive). | `string` |
| `sipAddresses` | Address provided by Webex Calling when the line is registered. | `string\[\]` |
| `voicemail` | Voicemail Pilot number for each line. | `string` |
| `lastSeen` | Last interaction of the line with Webex Calling. | `string` |
| `keepaliveInterval`   | Time interval after which the registration for a line expires. | `number` | 
| `callKeepaliveInterval` |  Interval within which the Calling SDK needs to send a ping to keep the call alive on Webex Calling. |`number` |
| `rehomingIntervalMin` |  The minimum interval for the Line to return to the primary Webex Calling server. |`number` |
| `rehomingIntervalMax` | The maximum interval for the Line to return to the primary Webex Calling server. | `number` |
| `voicePortalNumber` | Reserved for Webex Contact Center. | `number` |
| `voicePortalExtension` | Reserved for the Webex Contact Center. | `number` |
