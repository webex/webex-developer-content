---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Activation
- Activation Flow
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
