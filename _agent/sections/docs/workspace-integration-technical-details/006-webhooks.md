---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Activation
- Webhooks
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/workspace-integration-technical-details). [Full Markdown](../../../../docs/workspace-integration-technical-details.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide describes the technical details and syntax for the manifest, OAuth, and notification messages.

---

Follow the steps below to set up a new `org_private` Workspace Integration. Every step is detailed further below in this guide.

1. Describe the application in a manifest file and upload it in Control Hub. This gives you an OAuth client ID and a client secret. For further details, see [The Integration Manifest](https://developer.webex.com/docs/workspace-integration-technical-details#the-integration-manifest) for information regarding the manifest, and [Deployment](https://developer.webex.com/docs/workspace-integration-technical-details#deployment) to make the integration available for customers to activate.
2. Receive an activation JWT. If the manifest specified the manual provisioning flow, this happens by an admin activating the integration in Control Hub and copy-pasting the JWT to your integration, as described in [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).
3. Use the OAuth credentials from step 1 and the credentials from step 2 to update the integration status, as described in step 4 of [Activation](https://developer.webex.com/docs/workspace-integration-technical-details#activation).

    At this point, you have everything you need to start interacting with the Webex APIs.

4. Implement the rest of the Workspace Integrations protocol.
5. Use your credentials to interact with the Webex APIs in order to implement your functionality.

To create a _public_ integration there are some additional steps, such as that the manifest needs to be approved and deployed by Cisco, as detailed in the sections below.



> **Info**
>
> Analytics, Meeting and XSI scopes do not currently work with Workspace Integrations.

## Parent context

## Activation

Activating an integration ultimately means to provide the integration with the details needed to integrate with the Webex APIs. Administrators do this in Control Hub via the "Activate" button.

These details are in both modes of provisioning encoded in a Cisco signed JSON Web Token ([JWT](https://datatracker.ietf.org/doc/html/rfc7519)), in Control Hub named an _activation code_:

1. **Manual**: The JWT is copied from Control Hub UI and must be manually provided to the integration.
2. **HTTPS**: The JWT is transported in an HTTPS POST request to the URL specified in the provisioning part of the manifest.

![activation](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt71d25a6f2b6ddfe6/64526bc526dc891182facd4a/activation-code.png)

The JWT uses the _ES256_ algorithm and an _ECDSA_ signature. To verify the signature, the JSON Web Key Set (JWKS) can be found at the following regional URLs:



| Region | Description | URL                                  |
| ----- | ------------ |--------------------------------------|
| `us-west-2_r` | US West (Oregon) | https://xapi-r.wbx2.com/jwks         |
| `us-east-2_a` | US East (Ohio) | https://xapi-a.wbx2.com/jwks         |
| `eu-central-1_k` | Europe (Frankfurt) | https://xapi-k.wbx2.com/jwks         |
| `me-central-1_d` | Middle East (UAE) | https://xapi-d.wbx2.com/jwks         |
| `us-gov-west-1_a1` | Webex for Government (FedRAMP) | https://xapi.gov.ciscospark.com/jwks |

The `region` key is embedded in the JWT and can be used to lookup the correct JWKS URL. If a region is found in the JWT that does not match one of the entries in this list (excluding `us-gov-west-1_a1`), default to the `us-east-2_a` URL: https://xapi-a.wbx2.com/jwks.
The Webex for Government (FedRAMP) should default to the `us-gov-west-1_a1` region URL: https://xapi.gov.ciscospark.com/jwks.

## Selected section

### Webhooks

If a webhook was specified during activation, it will receive notifications for supported status and event keys that the integration has been granted access to (access is granted through the `xapiAccess` part of the manifest). 

Note that change notifications are only supported for shared devices (devices in workspaces). Personal devices are currently not supported.

The following keys are supported:

#### Supported Events



| Frequency | Event keys                                                                                                                                                                                                                      |
| ----- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sent immediately when raised | `Bookings.Start`, `Bookings.End`, `Bookings.ExtensionRequested`, `Bookings.Deleted`, `BootEvent`, `CallDisconnect`, `CallSuccessful`, `OutgoingCallIndication`, `UserInterface.Message.Prompt.Response`, `UserInterface.Message.Prompt.Cleared`, `UserInterface.Message.Rating.Response`, `UserInterface.Message.Rating.Cleared`, `UserInterface.Message.TextInput.Response`, `UserInterface.Message.TextInput.Clear`, `UserInterface.Extensions.Panel.Clicked`, `UserInterface.Extensions.Panel.Close`, `UserInterface.Extensions.Widget.Action`, `UserInterface.Assistant.Notification`, `UserInterface.WebView.Display`, `UserInterface.WebView.Cleared` |

#### Supported Status



| Frequency | Status keys                                                                                                                                                                                                                                                                                                                                                                                   |
| ----- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sent immediately when the value changes | `Standby.State`, `SystemUnit.State.NumberOfActiveCalls`, `Conference.Presentation.LocalInstance[*].SendingMode`,`RoomAnalytics.Engagement.CloseProximity`,`RoomAnalytics.PeoplePresence`,`RoomAnalytics.PeopleCount.Current`, `RoomAnalytics.T3Alarm.Detected`, `SystemUnit.State.System`, `MicrosoftTeams.Calling.InCall`, `MicrosoftTeams.Pairing.Active`, `MicrosoftTeams.User.SignedIn`                                             |
| Sent at most every minute | `Bookings.Availability.Status`                                                                                                                                                                                                                                                                                                                                                                |
| Sent at most every 5 minutes | `RoomAnalytics.AmbientNoise.Level.A`, `RoomAnalytics.AmbientTemperature`, `Peripherals.ConnectedDevice[*].RoomAnalytics.AmbientTemperature`, `RoomAnalytics.RelativeHumidity`, `Peripherals.ConnectedDevice[*].RoomAnalytics.RelativeHumidity`, `RoomAnalytics.Sound.Level.A`, `Peripherals.ConnectedDevice[*].RoomAnalytics.AirQuality.Index`, `RoomAnalytics.ReverberationTime.Middle.RT60` |

A notification is only sent if the value has changed since the last notification. If the value has been unchanged for longer than the defined max frequency, a notification is sent immediately once it changes. If the value changes multiple times during the notification period, the notification will only contain the last value.

Note that the `RoomAnalytics` data is only sent if the customer has opted into Workspace Utilization data and/or Workspace Environmental data in Control Hub (these settings are configured under "Workspaces > Settings").

#### Example Webhook Request

Let's have a look at an example webhook request and the fields.

```http
POST {webhook.targetUrl}
X-Spark-Signature: [... HMAC-SHA1 of the body using the webhook.secret ...]
{
  "appId": "ac6b6972-538e-11ec-bf63-0242ac130002",
  "deviceId": "Y2lzY29[...]MjZiYzZm",
  "workspaceId": "Y2lzY29zcGF[...]NjM=",
  "orgId": "Y2lzY29[...]YzVj",
  "timestamp": "1970-01-01T00:00:10Z",
  "type": "status",
  "changes": {
    "updated": {
      "Standby.State": "Halfwake",
      "RoomAnalytics.PeopleCount.Current": 2
    },
    "removed": [
      "Audio.Microphones.Mute"
    ]
  },
  "isFullSync": false
}
```

#### Fields That Are Present in Both Status and Event Messages



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `appId` | Required | String | The integration ID. |
| `deviceId` | Required | String | The device ID. |
| `workspaceId` | Required | String | The workspace ID. Not present in health check messages. |
| `orgId` | Required | String | The customer ID. Corresponds to the `sub` in the activation JWT. |
| `timestamp` | Required | Timestamp | ISO8601 UTC date time when this message was sent. |
| `type` | Required | `status`, `events` or `healthCheck` | The type of webhook message. In this case a _status_ change notification. |

#### Fields That Are Only Present When Type is Status



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `changes` | Required | Object | Object containing the updated or removed status keys |
| `changes.updated` | Optional | Object | Object containing the updated status keys. In the example above, the standby state and the people count values changed. |
| `changes.removed` | Optional | Array | List of status keys that are no longer present. In the example above, the microphones are no longer muted. |
| `isFullSync` | Required | Boolean | If true, this is an update containing the current state for the subscribed status values. This means that the update was not necessarily triggered by a status change; approximately every hour the devices will send out a "full sync" containing the relevant status keys. |

#### Fields That Are Only Present When Type is Events



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `events` | Required | Array | List of events that have been triggered. |
| `events.key` | Required | String | Name of the event. |
| `events.value` | Required | Object | Object containing any additional event data. |
| `events.timestamp` | Required | Timestamp | ISO8601 UTC date time the event occurred at. |

#### Webhook Message Authentication

Webhook messages support three forms of authentication:

- HMAC verification: an HMAC (HMAC-SHA1) of the entire webhook payload is computed using the value in the `secret` field as the key and sent in the `X-Spark-Signature` header. The recipient must also compute this value and verify that the message is signed with the shared webhook secret. If the `timestamp` is older than _5 minutes_, the message must be discarded to avoid replays of old, but valid messages.
- HTTP basic authentication: the `username` and `password` fields are used as credentials with HTTP basic authentication.
- Custom authentication token: the value of the `secret` field is sent in the `Authorization` header.

HMAC verification is the recommended authentication strategy. Secrets should also be changed periodically, which the integration can do in a new patch to the `appUrl`. The new configuration will apply approx. 5 minutes after it is updated.

#### Webhook Health Check

To verify that the webhook is working as expected, a payload of type `healthCheck` may also be sent. This payload allows Cisco to verify that webhooks are being correctly received on the integrator side. Messages should be authenticated by verifying the contents of the `X-Spark-Signature` or `Authorization` header, depending on the authentication strategy. If verification succeeds, the integration should respond with a 200 OK.

```http
POST {webhook.targetUrl}
X-Spark-Signature: [... HMAC-SHA1 of the body using the webhook.secret ...]
{
  "appId": "ac6b6972-538e-11ec-bf63-0242ac130002",
  "timestamp": "1970-01-01T00:00:10Z",
  "type": "healthCheck" // standard payloads have type = 'status'
}
```

#### Removing a Webhook

To remove a webhook, an update (PATCH) needs to be applied, with a webhook type `none`:

```http
PATCH {appUrl}
Authorization: Bearer {access_token}
{
  "webhook": {
    "type": "none"
  }
}
```
