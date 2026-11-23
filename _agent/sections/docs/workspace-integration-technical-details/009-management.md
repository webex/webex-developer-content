---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Management
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

## Selected section

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
