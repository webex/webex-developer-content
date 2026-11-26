---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Activation
- Example Activation JWT
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
