---
type: Guide
title: Workspace Integration Technical Details
display_title: Technical Details
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
content_type: documentation
product_group:
- webex-suite
categories:
- create
- devices
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/workspace-integration-technical-details)

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



## The Integration Manifest

The integration manifest provides the metadata needed to understand the capabilities of the integration, what permissions it needs and how it should be provisioned. Let's have a look at an example and break down the fields:

### Example Manifest

```json
{
  "id": "ac6b6972-538e-11ec-bf63-0242ac130002",
  "manifestVersion": 1,
  "displayName": "ACME Device Integration",
  "vendor": "ACME INC.",
  "email": "example-app@example.com",
  "description": "The ACME integration will do magic with your Webex device sensor data",
  "descriptionUrl": "https://example.com/webexintegration/details",
  "tocUrl": "https://example.com/webexintegration/toc",
  "availability": "global",
  "apiAccess": [
    {
      "scope": "spark-admin:devices_read",
      "access": "required",
      "role": "id_readonly_admin"
    },
    {
      "scope": "spark-admin:workspaces_read",
      "access": "required",
      "role": "id_readonly_admin"
    },
    {
      "scope": "spark:xapi_statuses",
      "access": "required"
    },
    {
      "scope": "spark:xapi_commands",
      "access": "required"
    }
  ],
  "xapiAccess": {
    "status": [
      {
        "path": "RoomAnalytics.*",
        "access": "required"
      },
      {
        "path": "Peripherals.ConnectedDevice[*].RoomAnalytics.*",
        "access": "required"
      },
      {
        "path": "Standby.State",
        "access": "required"
      },
      {
        "path": "SystemUnit.State.NumberOfActiveCalls",
        "access": "required"
      }
    ],
    "commands": [
      {
        "path": "Message.Send",
        "access": "required"
      }
    ],
    "events": [
      {
        "path": "BootEvent",
        "access": "required"
      },
      {
        "path": "UserInterface.Message.Prompt.Response",
        "access": "required"
      }
    ]
  },
  "provisioning": {
    "type": "manual"
  }
}
```

This example describes an integration from ACME, INC. It's a _global_ integration, which means it will have to be approved and deployed by Cisco, and thus made available to any customer that wants to activate it. For customers building their own integrations, the _availability_ field would be set to _org_private_, allowing the manifest to be uploaded in Control Hub.

The _apiAccess_ shows four required scopes, that would give access to reading device and workspace details, reading statuses and executing commands for the Webex Devices over the [xAPI](https://roomos.cisco.com/docs/Introduction.md#the-xapi). The status, command and event details are specified in the _xapiAccess_. The example is requesting access to:

- All status under RoomAnalytics for both the device itself and the attached peripherals (like the Room Navigator), the device standby state and how many active calls the device has.
- The UserInterface.Message.Prompt.Display command that displays a prompt on the device screen with a title, text and up to five options for the user.
- Two events: the boot event that is sent when a device reboots and the UserInterface.Message.Prompt.Response following a selection by the user for the message prompt.

The provisioning section shows that the integration is deploy type _manual_, which means the Control Hub admin will need to copy an activation code and provide this to the integration.

This is how the manifest will render in Control Hub:

![Control Hub manifest](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea3a7c98898ec5ee/64526bc5f1b32a119f435022/control-hub-manifest.png)

### Manifest Details



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| `id` | Required | UUID | The Id of the integration. Generated by the integration developer, needs to be globally unique. |
| `manifestVersion` | Required | Integer | The manifest version. When the manifest changes, the version must be incremented. |
| `displayName` | Required | String | A display name for the integration |
| `vendor` | Required | String | The name of the vendor / company that created the integration |
| `email` | Required | String | An email address from the integration vendor |
| `description` | Required | String | A description of what the integration does and what value it will provide to the customer |
| `descriptionUrl` | Optional | String | A URL to a more detailed description of what the integration does and what value it provides to the customer |
| `tocUrl` | Required (when `global`) | URL | A URL to a web page listing the terms and conditions for the integration. The admin will have to accept these when enabling the integration from Control Hub. Note that this URL is not required for private integrations.
| `availability` | Required | `global` or `org_private` | Describes if the integration is `global` and available to all customers, or `org_private`, which means it only applies to a specific customer organization. Note that only `org_private` integrations can be manually uploaded by a Control Hub admin. `global` integrations are deployed by Cisco on behalf of the vendor. |
| `apiAccess` | Required | Array| A list of Webex API scopes the integration is requesting. These scopes allow access to specific public [Webex developer APIs](https://developer.webex.com/docs/getting-started). |
| `apiAccess.scope` | Required | String | The scope requested. See [Webex API scopes](https://developer.webex.com/docs/integrations#scopes) for examples. |
| `apiAccess.access`| Required | `required` or `optional` | Is the scope required or optional. Optional scopes can be opted out by the Control Hub admin. |
| `apiAccess.role` | Optional | `id_full_admin`, `id_readonly_admin` or `id_device_admin` | Some APIs require a specific use role to be assigned to the account created for the integration. For most read APIs, `id_readonly_admin` should be sufficient. Check the API docs for the specific APIs to see what roles, if any, are required. |
| `xapiAccess` | Required | Array | A list of device xAPI status, commands and events that the integration is requesting access to. See https://roomos.cisco.com/xapi for more details of what is supported by the Webex Devices |
| `xapiAccess.status.path` | Required | String | The status path requested. Wildcards indicate all statuses recursively under the specific path, say RoomAnalytics.* means all statuses under the RoomAnalytics node in the status tree.  |
| `xapiAccess.status.access`| Required | `required` or `optional` | Is the status required or optional? Optional statuses can be opted out by the Control Hub admin. |
| `xapiAccess.commands.path` | Required | String | The command(s) requested. Wildcards indicate all commands recursively under the specific path, say Bookings.* means all commands under the Bookings node in the command tree.  |
| `xapiAccess.commands.access` | Required | `required` or `optional` | Is the command required or optional. Optional commands can be opted out by the Control Hub admin. |
| `xapiAccess.events.path` | Required | String | The event requested. |
| `xapiAccess.events.access`| Required | `required` or `optional` | Is the event required or optional? Optional events can be opted out by the Control Hub admin. |
| `provisioning` | Required | Provisioning | Describes how the integration is provisioned when enabled from Control Hub |
| `provisioning.type` | Required | `manual` or `https` | `manual` provisioning means the Control Hub admin will be presented with an activation code that is copied and provided to the integration. `https` provisioning removes the need for the activation code but requires a global activation URL for the 3rd party service. More details on this later. |
| `provisioning.url` | Required (when `https`) | URL | If the type is `manual`, the URL is optional. If set, it provides a link to the page where the admin needs to provide the activation code. If the type is `https`, the URL is required and is where the activation code is posted to start the activation flow. Note that the URL must be an HTTPS URL.  |
| `provisioning.activationGuideUrl` | Optional | URL | Cannot be used together with `provisioning.url`. If specified, it provides a link to a documentation page by the integrator explaining how to continue the activation process. |

## Deployment

Deploying an integration will make it available for activation in Control Hub. Private integrations will only be accessible to the integration developer organization, and can be uploaded in Control Hub by the administrator:

![Upload integration](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb9ca45dd15cdff10/64526bc53a6e3c10d270c49c/upload-integration.png)

Global integrations are approved and deployed by Cisco. They are available for all customers to activate through Control Hub. In both cases, the output of the process is an OAuth clientId and secret that the integration needs to get an access token to use in the Webex APIs.

![OAuth clientID and secret](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt86782cd1f8590aa6/64526bc5fb3d807d46df80e7/client-id-secret.png)

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

### Example JSON Web Key Set (JWKS)

```json
{
  "keys": [
    {
      "kty": "EC",
      "use": "sig",
      "crv": "P-256",
      "kid": "VkOd36xy3JeGFka5uW5gW525",
      "key_ops": [
        "verify"
      ],
      "x": "ilEKY13J464rnzK4CvdIh1_ow3q4e1eoqnjXES_PnC8",
      "y": "T-Kp8qcf4FBvvtNIMSkQmAWnbd3uiz2U_NqfTavc1x8",
      "alg": "ES256"
    },
    {
      "kty": "EC",
      "use": "sig",
      "crv": "P-256",
      "kid": "GzaEArXcMo24RDst1kP5r1q7",
      "key_ops": [
        "verify"
      ],
      "x": "vflTChGJ6bjxt2e4M3nIVb90IZb9Ms7fg0wcQ9FrFV0",
      "y": "07HeNRvKQW4b-JiAuvNoXc957flcH6PD538jhWTFvHI",
      "alg": "ES256"
    },
    {
      "kty": "EC",
      "use": "sig",
      "crv": "P-256",
      "kid": "m9vlvDThppHKT0LlQbeURKwd",
      "key_ops": [
        "verify"
      ],
      "x": "h0rF6Q0EZXQsAGmNG-S7Dnw29LEpDE3lGj_FNOYoRJc",
      "y": "td1qLYMGXK9m4PqKF4cdrHMPoeU-g9pmPQGsGTnhSFU",
      "alg": "ES256"
    }
  ]
}
```

### Example Activation JWT

Let's have a look at an example JWT activation code and break down the fields. You can find more details on the JSON Web Token standard in [RFC7519](https://datatracker.ietf.org/doc/html/rfc7519). The JWT is a string with three dot separated _base64url encoded_ strings:

`header.payload/claims.signature`

```text
Encoded:

<BASE64URL_ENCODED_HEADER>
.
<BASE64URL_ENCODED_PAYLOAD>
.
<BASE64URL_ENCODED_SIGNATURE>

Decoded:

Header:
{
  "kid": "<KEY_ID>",
  "typ": "JWT",
  "alg": "ES256"
}
Payload:
{
  "sub": "<ORGANIZATION_ID>",
  "oauthUrl": "https://webexapis.com/v1/access_token",
  "orgName": "Example Organization",
  "appUrl": "https://example.com/workspace-integration",
  "userId": "<USER_ID>",
  "manifestUrl": "https://example.com/workspace-integration/manifest.json",
  "appId": "<WORKSPACE_INTEGRATION_ID>",
  "expiryTime": "2023-08-10T08:02:33.816114574Z",
  "action": "provision",
  "webexapisBaseUrl": "https://webexapis.com/v1",
  "scopes": "spark-admin:devices_read,spark:xapi_statuses,spark-admin:workspaces_read,spark:xapi_commands",
  "region": "us-east-2_a",
  "iat": 1691568153,
  "jti": "<JWT_ID>",
  "refreshToken": "<WORKSPACE_REFRESH_TOKEN>",
  "xapiAccess": "{\"commands\":[\"Message.Send\"],\"statuses\":[\"RoomAnalytics.*\",\"Peripherals.ConnectedDevice[*].RoomAnalytics.*\",\"SystemUnit.State.NumberOfActiveCalls\",\"Standby.State\"],\"events\":[\"UserInterface.Message.Prompt.Response\",\"BootEvent\"]}"
}
Signature:
<BASE64URL_ENCODED_SIGNATURE>
```



| Field | Required / Optional | Value space                                                          | Description |
| ----- | ------------------- |----------------------------------------------------------------------|------------ |
| `kid`| Required | String                                                               | The Id of the key from the JSON Web Key Set (JWKS) used to sign this JWT |
| `typ` | Required | String                                                               | Will be _JWT_ for our use  case here |
| `alg` | Required | String                                                               | Specifies the signature algorithm used to sign the key: _ES256_ which means ECDSA using P-256 and SHA-256. |
| `sub` | Required | String                                                               | The Webex customer / organization ID. |
| `oauthUrl` | Required | URL                                                                  | The URL to fetch an OAuth access token from the provided refresh token |
| `orgName` | Required | String                                                               | The name of the Webex customer / organization |
| `region`| Required | `us-west-2_r`, `us-east-2_a`, `eu-central-1_k` or `us-gov-west-1_a1` | The region for the Webex customer. Should be used to determine which JWKS URL to use. |
| `appUrl` | Required | URL                                                                  | The URL to use to patch details about the integration, like actionUrl, webhookUrl and more. |
| `manifestUrl` | Required | URL                                                                  | URL containing the integration's latest manifest. |
| `appId` | Required | UUID                                                                 | The Id of the integration, same as in the manifest |
| `expiryTime` | Required | Timestamp                                                            |  ISO8601 UTC date time when this request will expire. If an integration receives a JWT after this date, it should be refused. The expiry is 24 hours. |
| `action` | Required | String                                                               | The type of action this JWT embeds, which in the activation case is `provision` |
| `webexapisBaseUrl` | Required | URL                                                                  | The base URL for the Webex public APIs. Append the specific API urls (e.g. `v1/workspaces`, `v1/xapi/status`) to this base URL. |
| `iat` | Required | NumericDate                                                          |  The [issued at](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1.6) field identifies the time at which the JWT was issued. |
| `jti` | Required | String                                                               | The [JWT ID](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1.7) field provides a unique identifier for the JWT. The jti is used to prevent replays of the same message. Integrators should disallow a JWT with a jti that has been seen within the last 24 hours (which is the expiry time of the message). After 24h, a replay will be invalidated by the expiry time. |
| `refreshToken` | Required | String                                                               | The OAuth refresh token. This token can be used to get an access token from the oauthUrl. |
| `scopes` | Required | String                                                               | A comma separated list of scopes granted. If the manifest has optional scopes, this shows what scopes got approved. |
| `xapiAccess` | Required | Object                                                               | The xAPI commands and statuses granted. If the manifest has optional status or commands, this shows which got approved. |

### Activation Flow

#### 1. a) Provide Activation Code JWT (Manual)

The activation code JWT is copied from Control Hub and provided to the integration.

#### 1. b) Provide Activation Code JWT (HTTPS)

The JWT is sent in an HTTPS POST (the payload is the same as for the manual case) to the URL provided in the provisioning part of the manifest. At this point, there is no association with the tenant / customer on the integrators side, which means the activation data will have to be stored temporarily with an activation session id embedded in the redirect URL returned. The response must contain said redirect URL in the success case or a detailed (human friendly) error if something goes wrong.

The redirect URL should be a landing page in the 3rd party integration that can authenticate the admin (in case they have an existing account) or allow the creation of a new user. When the admin is authenticated in the 3rd party system, the association between the Cisco activation JWT posted earlier and the 3rd party account can be made (including any additional 3rd party setup needed). The Cisco customer details from the JWT (orgName) can be used to render what customer from Webex the activation applies to.

```http
POST https://example.com/webexintegration
{
  "jwt": "eyJhbGciOiJFUzI1NiJ9...."
}

Response 200 OK:
{
  "redirectUrl": "https://example.com/webexintegration/setup/81dc908d-39a1-4a11-9dd1-43ab22d1d571"
}

Response 5XX/4XX:
{
  "description": "A human friendly description of the failure",
  "trackingId": "an-error-reference-to-provide-to-support"
}
```

#### 2. Validate the Activation JWT

When the integration has received the activation JWT, it needs to be validated:

1. Read the `region` field from the JWT (prior to validation) and use it to select from the list of regional JSON Web Key Set (JWKS) URLs described earlier. If no match, default to the `us-east-2_a` URL except for Webex for Government (FedRAMP) region which should default to the `us-gov-west-1_a1` URL. Fetch the JWKS from the URL.
2. Verify the ES256 signature using the the JWKS. The `kid` in the JWT header indicates what key to use from the key set. If there is no matching key in the key set, the JWT should be considered invalid.
3. If the signature is valid, the integration should look at the `expiryTime`. If the current time _is after_ this timestamp, the JWT is invalid and cannot be used for activation.
4. The integration must look at the `appId` and verify that it matches the id provided in the app manifest.
5. Store the `jti` for up to 24 hours and reject any JWT that contains the same ID at a later point in time.

#### 3. Verify and Store the Activation Payload

The most important part of the activation payload is the `refreshToken`. The integration should verify that the token can be exchanged for a valid access token using the `oauthUrl` from the JWT and the client ID and client secret from the deployment step:

```http
POST {oauthUrl}
{
  "grant_type": "refresh_token",
  "client_id": "... from deployment ...",
  "client_secret": "... from deployment ...",
  "refresh_token": "... from the JWT ..."
}

Response 200 OK:
{
  "expires_in": 7199,
  "token_type": "Bearer",
  "refresh_token": "<WEBEX_REFRESH_TOKEN>",
  "refresh_token_expires_in": 5090490,
  "access_token": "eyJhbGciOiJSUzI1NiJ9..."
}
```

The `access_token` is the token to use in all requests to the Webex APIs added to the _Authorization HTTP header_, but do note that it has an expiry and when expired, the integration must fetch a new access token using the refresh token:

`Authorization: Bearer eyJhbGciOiJSUzI1NiJ9...`

Also note that if the POST returns a new `refresh_token` (not the same as the one in the JWT), _update to use the one returned from the oauthUrl post_.

When the refresh token has been validated, the details from the payload needs to be securely stored and associated with the 3rd party tenant account (if applicable).

#### 4. Update the Integration Activation Status

If the setup is completed on the 3rd party integrations side, this fact must be passed on by a PATCH to the `appUrl` from the manifest (using the access token from the previous step), together with the customer specific `actionsUrl`. The `actionsUrl` is where Webex will send JWT encoded actions to the integration. Note that the `actionsUrl` is optional, but not having one will significantly impair the management capabilities (no Webex initiated re-provisioning, updates, health checks etc.).

The integration can also pass in either a `webhook` or a `queue` definition that will allow receiving xAPI status changes and the integration customer details.

```http
PATCH {appUrl}
Authorization: Bearer {access_token}
{
  "provisioningState": "completed",
  "actionsUrl": "https://eu.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/webexintegration/actions",
  "webhook": {
    "targetUrl": "https://eu.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/webexintegration/sendmedata",
    "type": "hmac_signature",
    "secret": "my-secret-key-for-signing"
  },
  "queue": {
    "state": "enabled"
  },
  "customer": {
    "id": "tenant / customer ID",
    "name": "display name of the tenant / customer"
  }
}
```



| Field             | Required / Optional | Value space                                                              | Description                                                                                                                                                         |
|-------------------|--------------------|--------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `provisioningState` | Required           | `completed` or `error`                                                   | The state of the provisioning / activation                                                                                                                          |
| `actionsUrl`        | Optional           | URL                                                                      | The URL where Webex will send JWT encoded actions. Must be an HTTPS URL with a valid certificate and publicly available.                                            |
| `webhook`           | Optional           | Object                                                                   | Specifies a webhook to receive xAPI change notifications                                                                                                            |
| `webhook.targetUrl` | Required           | URL                                                                      | The URL where the status change notifications will be posted. Must be an HTTPS URL with a valid certificate and publicly available.                                 |
| `webhook.type`      | Required           | `hmac_signature`, `basic_authentication`, `authorization_header`, `none` | The webhook authentication strategy to use. Passing `none` will delete the webhook.                                                                                 |
| `webhook.secret`    | Optional           | String                                                                   | The secret to use with the `hmac_signature` or `authorization_header` strategies. Must be 20 characters or longer.                                                  |
| `webhook.username`  | Optional           | String                                                                   | The username to use with the `basic_authentication` authentication strategy.                                                                                        |
| `webhook.password`  | Optional           | String                                                                   | The password to use with the `basic_authentication` authentication strategy.                                                                                        |
| `queue`             | Optional           | Object                                                                   | Specifies a message queue to receive xAPI change notifications                                                                                                      |
| `queue.state`       | Required           | `enabled`, `disabled` or `remove`                                        | If `enabled`, a queue will be created for the integration. Passing `disabled` will turn off notifications for an existing queue and `remove` will delete the queue. |
| `queue.pollUrl`     | Required           | URL                                                                      | If the queue is `enabled`, the patch response will contain the URL to poll for messages.                                                                            |
| `customer`          | Optional           | Object                                                                   | The tenant / customer details from the 3rd party integration side                                                                                                   |
| `customer.id`       | Required           | String                                                                   | The Id of the customer from the integration                                                                                                                         |
| `customer.name`     | Optional           | String                                                                   | The display name of the customer from the integration                                                                                                               |

At this point we should have a functioning integration and Control Hub will show the integration as active.

Note that the patch response contains the current integration details, including the queue poll URL if a message queue is enabled.

<a id="webhooks"></a>

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

### Queues

If a queue was enabled during activation, it will receive notifications for supported status and event keys that the integration has been granted access to, and the `updateApproved` action described in the Management section. The message payload and supported statuses / events are the same as described for webhooks, but the delivery is done by HTTP long polling the `pollUrl`, rather than providing a webhook URL.

The advantages with the message queue based approach are:

1. There is no webhook infrastructure needed. The integration only needs to do outbound HTTP GET requests to read messages from the queue.
1. The message retention is 10 minutes, so an integration can have a short downtime and not lose messages.

#### Queue Polling

Let's have a look at an example queue poll request and the message response.

```http
GET {queue.pollUrl}
Authorization: Bearer {access_token}
Response:
{
  "messages": [
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
        "removed": []
      },
      "isFullSync": false
    }
  ]
}
```

The payload returned from the message queue is the same as described for webhook posts, but listed in a messages array. A message poll request will:

1. Return from 0 to a maximum of 10 messages.
1. Wait for up to 20 seconds for messages to be written to the queue. If no messages, the request will return with an empty messages array after 20 seconds.

Note that the message retention is 10 minutes, so a message that is written to the queue and not fetched within this timeframe will automatically be deleted.

The recommended behavior for the queue polling is to do it continuously in a loop for as long as the integration is running. Any failures should trigger a wait until the next poll attempt.

```Java
while (running) {
   try {
       QueuePollResponse response = webexHttp.get(queueUrl, QueuePollResponse.class);
       doSomethingWith(response.getMessages());
   } catch (Exception ex) {
        // An unexpected error, wait 10 seconds before trying another poll
       sleep(10000);
   }
}
```

#### Removing the Queue

To remove a queue, an update (PATCH) needs to be applied, with a queue state of `remove`:

```http
PATCH {appUrl}
Authorization: Bearer {access_token}
{
  "queue": {
    "state": "remove"
  }
}
```

### Caching of Notifications

Please note that long polling and webhook details are cached and it can take up to 10 minutes for data to start flowing after changing.

## Management

The integrations framework defines APIs and messages for the management of an integration beyond the initial activation and setup. This is important to manage the life cycle of the integration, from verifying status / health, updating the authorization tokens and to deactivating the integration.

The management APIs can be divided in two:

1. Webex to integration: Signed JWTs similar to the one used in the activation flow that requests the integration to perform certain actions. These can be posted to the provided `actionsUrl`, or in the case of a re-provision, provided manually to the activation.
1. Integration to Webex: HTTP GET or PATCH of the `appUrl`.

Let's have a look at these in more detail:

### Actions: Webex to Integration

The _actionsUrl_ provided by the integration is used to send signed JWT "actions". All the JWT payloads are signed the same way as the activation request (ES256 and ECDSA):

```http
POST {actionsUrl}
{
  "jwt": "eyJhbGciOiJFUzI1NiJ9...."
}
```

The actions supported are as follows:

#### Health Check

Run a health / connectivity check for the integration. This allows Webex to check the current state and detect if the integration has been removed on the integrator side without a successfully completed removal flow (indicated by the integration returning 404 Not Found or 410 Gone). Note that the most important part of this check is for the integration to verify that it is able to talk to the Webex APIs and report a _tokensState_. The token state behavior should be as follows:

- **valid**: The integration can successfully do a GET on the appUrl with a 200 OK
- **invalid**: A GET on the appUrl returns a 401 / 403 and the app is unable to get a new access token from the refresh token. The fix will be to provision a new refresh token via the "update" action.
- **unknown**: A GET on the appUrl fails with a non 200/401/403 status or a transient network issue (timeout etc.)

The _operationalState_ can indicate other problems with the integration and the Control Hub admin will be guided to log in to check the state.

```text
Request (JWT)
{
  "sub": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8zYTZmZjM3My02OGE3LTQ0ZTQtOTFkNi1hMjc0NjBlMGFjNWM",
  "iat": 1516239022,
  "jti": "WTJselkyOXpjR0Z5YXpvdkw=",
  "appId": "6d93fe09-7130-4507-b261-3908b63428a4",
  "action": "healthCheck"
}

Response:
{
  "operationalState": "operational",
  "tokensState": "valid"
}
```



| Field | Required / Optional | Value space | Description |
| ----- | ------------------- | ----------- |------------ |
| operationalState | Required | `operational`, `impaired` or `outage`| The operational state of the integration. If the integration is not operational, it can report either `impaired` to indicate that some features might not work or `outage` to indicate a full outage for all integration features. |
| tokensState| Required | `valid`, `invalid` or `unknown`| The state of the auth tokens. Should be verified by doing an HTTP GET of the `appUrl`. |

If the integration uses webhooks, a `healthCheck` type payload is also sent to the webhook URL to verify that it is working correctly.

#### Update

1. The `appUrl`, `manifestUrl` and the `region` can change, for example when the Webex customer is moved to a different region. The token will be sent to the `actionsUrl` if provided. If the integration uses the manual activation flow, administrators can generate a new JWT after migration to the new region. Cluster changes will revoke the existing refresh token, so integrations should let administrators provide this action JWT to the integration so that it can continue interacting with Webex APIs as before.
1. A new refresh token can be provided, if needed.

```text
Request (JWT)
{
  "sub": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8zYTZmZjM3My02OGE3LTQ0ZTQtOTFkNi1hMjc0NjBlMGFjNWM",
  "iat": 1516239022,
  "jti": "WTJselkyOXpjR0Z5YXpvdkw=",
  "appId": "6d93fe09-7130-4507-b261-3908b63428a4",
  "action": "update",
  "appUrl": "https://xapi-k.wbx2.com/xapi/api/organizations/3a6ff373-68a7-44e4-91d6-a27460e0ac5c/apps/6d93fe09-7130-4507-b261-3908b63428a4",
  "manifestUrl": "https://xapi-k.wbx2.com/xapi/api/organizations/3a6ff373-68a7-44e4-91d6-a27460e0ac5c/appManifests/6d93fe09-7130-4507-b261-3908b63428a4",
  "region": "eu-central-1_k",
  "refreshToken": "eyJhbGciOiJSUzI1NiJ9..."
}

Response 204 No content
```

#### Update Approved

The `updateApproved` action is sent when the admin has approved an update to a new manifest version. For convenience, the message contains the scopes and xApi access approved from the new manifest (including any optional ones).

When this message is received, the refresh token will already support the new API scopes and the integration can fetch a new access token to start using the new Webex APIs.

Note that in the case this message is lost, the integration can still check the current state by doing an HTTP GET request on the appUrl.

```text
Request (JWT)
{
  "sub": "Y2lzY29zcGFyazovL3VybjpURUFNOnVzLWVhc3QtMV9pbnQxMy9PUkdBTklaQVRJT04vM2E2ZmYzNzMtNjhhNy00NGU0LTkxZDYtYTI3NDYwZTBhYzVj",
  "iat": 1629278630,
  "jti": "v0wyEuKHTxygQB53-h8_qw==",
  "action": "updateApproved",
  "manifestVersion": "3",
  "appId": "a9aecf7e-af2c-48e7-ae61-3f49773922b1",
  "scopes": "spark-admin:workspaces_read,spark:xapi_statuses",
  "xapiAccess": {"commands": [], "statuses": ["RoomAnalytics.*"], "events": []}
}

Response 204 No content
```

#### Deactivate

Deactivate or `deprovision` the integration. When this action is received, the integration should be removed and terminated. If the delete is _interactive_, an optional `redirectUrl` can be provided to render a landing page for the customer to perform additional cleanup or capture other information.

```text
Request (JWT)
{
  "sub": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8zYTZmZjM3My02OGE3LTQ0ZTQtOTFkNi1hMjc0NjBlMGFjNWM",
  "iat": 1516239022,
  "jti": "WTJselkyOXpjR0Z5YXpvdkw=",
  "appId": "6d93fe09-7130-4507-b261-3908b63428a4",
  "action": "deprovision",
  "interactive": true
}

Response 200 (with redirectUrl) / 204 No content (if not):
{
  "redirectUrl": "https://eu.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/apps/6d93fe09-7130-4507-b261-3908b63428a4/removed"
}
```

### Integration to Webex (appUrl)

#### Update the integration

1. The `actionsUrl` can be updated in case there is a need to do so from the integrator.
2. Request a manifest update by adding a new `manifest.updateRequest`. An update request will trigger a flow where the admin can approve the update to a new version of the manifest including any changes to the permissions needed.

Note that an update request patched as described below _will only apply to this customer_. For global integrations, this can be used to roll out changes to Beta / Trial customers first, and when ready, Cisco will deploy the new manifest for all remaining customers.

```http
PATCH {appUrl}
Authorization: Bearer {access_token}
{
  "actionsUrl": "https://us.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/apps/6d93fe09-7130-4507-b261-3908b63428a4",
  "updateRequest": {
    "newManifest": { ... desired manifest for approval (as described in the manifest section) ... }
  }
}
```

#### Read the current integration state

Reading the current state allows the integration to:

1. Check the current integration manifest (including the version of the integration the customer has running) and trigger an update request if needed. An ongoing update request is indicated by the `updateRequest` object with the new manifest and the update state.
1. Detect if the integration has been removed on the Webex side without a successfully completed removal flow (indicated by a 404 Not Found or 410 Gone response code). This should trigger cleanup and removal of the integration setup on the integrators side.
1. Check what scopes and xAPI access the integration was granted, in case the manifest had optional values.
1. Verify that the `actionsUrl` is correct.

```http
GET {appUrl}
Authorization: Bearer {access_token}
{
  "id": "ac6b6972-538e-11ec-bf63-0242ac130002",
  "manifestVersion": 2,
  "scopes": [
    "spark:xapi_statuses",
    "spark:xapi_commands"
  ],
  "xapiAccessKeys": {
    "commands": [
      "Message.Send"
    ],
    "statuses": [
      "RoomAnalytics.*",
      "Standby.State"
    ]
  },
  "createdAt": "2021-10-27T08:48:26.232928Z",
  "updatedAt": "2021-11-19T11:26:50.209904Z",
  "provisioningState": "completed",
  "actionsUrl": "https://eu.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/webexintegration/actions",
  "webhook": {
    "targetUrl": "https://eu.example.com/customer/0beaca8b-3342-4eb4-973f-de70c14f2c91/webexintegration/sendmedata"
  },
  "customer": {
    "id": "tenant / customer ID",
    "name": "display name of the tenant / customer"
  }
}
```

## Security

Security is very important to Cisco and our customers and it's crucial that integrators focus on security when writing the integration.
Please have a look at the following security guidelines as you plan and review the implementation of your integration:



| Item | Description  |
| ---- | ------------ |
| Validate all JSON Web Tokens (JWT) | Make sure to verify the signature of the JWT and reject any JWTs where the `jti` (ID) has been seen before or where the `appId` does not match the appId provided by the integration in the manifest. In the case of the activation JWT (action: provision), reject any JWT where the `expiryTime` has passed. For any other JWT action type, an `iat` older than 5 minutes should be rejected. |
| Validate webhook authenticity | HMAC verification is the preferred authentication strategy. Always compute the HMAC-SHA1 for the webhook payload and assert that it is the same as the provided `X-Spark-Signature` HTTP header, or verify the contents of the `Authorization` header if basic authentication or a token is used.  |
| Protect the webhook secret | Use webhook secrets that are _unique per customer_. Also consider rotating / changing the secret periodically. If you do implement a secret rotation, do note that you need to accept payloads signed with both the old and the new secret for up to 5 minutes after the change. |
| Secure the webhook and JWT action transport | Both the webhook and action URLs must be HTTPS with a valid certificate signed by a trusted Certificate Authority. Self-signed certificates are not supported. |
| Minimize required xAPI access | Try to minimize the xAPI access required in your manifest. It's tempting to use wildcards to avoid having to specify individual statuses or commands, but this makes it a lot harder for the admin to know and understand what the integration is actually allowed to do. |
| Securely store data | All data received by the integration should be securely stored and encrypted at rest. This holds especially true for the `clientId`, `clientSecret` and `refreshToken`. |
