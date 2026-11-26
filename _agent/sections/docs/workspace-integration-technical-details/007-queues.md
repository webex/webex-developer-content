---
type: Excerpt
canonical_url: https://developer.webex.com/docs/workspace-integration-technical-details
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Activation
- Queues
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
