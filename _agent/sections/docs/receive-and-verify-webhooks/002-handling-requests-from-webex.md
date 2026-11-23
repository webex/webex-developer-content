---
type: Excerpt
canonical_url: https://developer.webex.com/docs/receive-and-verify-webhooks
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Handling Requests from Webex
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/receive-and-verify-webhooks). [Full Markdown](../../../../docs/receive-and-verify-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Receive Webex Webhooks API notifications, verify signatures over the original request bytes, and process accepted events without repeating side effects.

## Selected section

## Handling Requests from Webex

When one of your webhooks is triggered by an event, Webex will send an HTTP POST to the backend `targetUrl` that you've specified. The body of the POST will look something like this:

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1dFQkhPT0svZjRlNjA1NjAtNjYwMi00ZmIwLWEyNWEtOTQ5ODgxNjA5NDk3",
  "name": "New message in 'Project Unicorn' room",
  "resource": "messages",
  "event": "created",
  "filter": "roomId=Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
  "orgId": "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
  "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0MyNzljYjMwYzAyOTE4MGJiNGJkYWViYjA2MWI3OTY1Y2RhMzliNjAyOTdjODUwM2YyNjZhYmY2NmM5OTllYzFm",
  "ownedBy": "creator",
  "status": "active",
  "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "data":{
    "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvOTJkYjNiZTAtNDNiZC0xMWU2LThhZTktZGQ1YjNkZmM1NjVk",
    "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
    "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
    "personEmail": "matt@example.com",
    "created": "2015-10-18T14:26:16.000Z"
  }
}
```

The first few properties shown above are called the “envelope.” They identify all webhooks that are sent. This envelope contains the following information:



| Parameter   | Explanation                                                                                                                                                                                                                                                                            |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`        | The webhook ID. This is the same ID returned when you created the webhook and is what you would use to view the webhook configuration or delete the webhook.                                                                                                                           |
| `name`      | The name you gave your webhook when you created it.                                                                                                                                                                                                                                    |
| `resource`  | The resource the webhook data is about.                                                                                                                                                                                                                                                |
| `event`     | The type of event this webhook is for.                                                                                                                                                                                                                                                 |
| `filter`    | Lists any filters that you applied that triggered this webhook.                                                                                                                                                                                                                        |
| `orgId`     | The organization that owns the webhook. This usually is the organization the user that added the webhook belongs to. This ID can be used to [view the Organization details with the API](https://developer.webex.com/docs/api/v1/organizations/get-organization-details).                                                      |
| `createdBy` | The `personId` of the user that added the webhook.                                                                                                                                                                                                                                     |
| `appId`     | The ID of the Webex app that was used to create the webhook. This could be one of your apps, an app from the [Webex App Hub](https://apphub.webex.com), a privately developed app, or this Webex for Developers site if the webhook was created with your personal access token. Webex App Hub is not supported for Webex for Government (FedRAMP). |
| `ownedBy`   | Indicates if the webhook is owned by the *org* or the *creator*. Webhooks owned by the creator can only receive events that are accessible to the creator of the webhook. Those owned by the organization will receive events that are visible to anyone in the organization.          |
| `status`    | Indicates if the webhook is active. A webhook that cannot reach your URL is disabled. Thus, for all webhooks you receive, the status will always read ‘active.’                                                                                                                        |
| `actorId`   | The `personId` of the user that caused the webhook to be sent. For example, on a *messsage created* webhook, the author of the message will be the actor. On a *membership deleted* webhook, the actor is the person who removed a user from a room.                                   |
| `data`      | Contains the JSON representation of the resource that triggered the webhook. **Note:** Use the documented organization field for the operation you are performing. For Service App authorization, use `data.authorizerOrgId` to identify the authorizing customer; see [Service App authorization](https://developer.webex.com/docs/contact-center-service-apps#service-app-creation-developer-flow).                  |

<a id="using-the-data-property"></a>

### Using the Data Property

The webhook's `data` property contains the JSON representation of the resource event that triggered the webhook. For example, if you created a webhook that triggers when `messages` are `created` (i.e. posted into a room), then the `data` property will contain the JSON representation for a message resource, as specified in the [Messages API](https://developer.webex.com/docs/api/v1/messages) documentation.  Likewise, if you created a webhook that triggers when `telephony_calls` are `created` (i.e. a call is originated or received), then the `data` property will contain the JSON representation for a telephony_calls resource, as specified in the [Call-Control API](https://developer.webex.com/docs/api/v1/call-controls) documentation.

If the webhook's resource event contains sensitive data, the data property will only contain “metadata” about the event. See [Handling Sensitive Data](https://developer.webex.com/docs/receive-and-verify-webhooks#handling-sensitive-data) for more information about how to retrieve the entire resource.

<a id="handling-sensitive-data"></a>

### Handling Sensitive Data

Webex encrypts sensitive room content such as titles and message text using keys only available to the members of that room. This means that not even the Webex operations team can read your messages, This affects the resource data included in webhook notifications.

You'll notice in the above message webhook example that the `text` property is missing. That's because room messages are considered sensitive information and since Webex initiated the request to your backend, it did not have your Access Token with which to decrypt the message. In order to get the sensitive information, your app needs to use the resource `id` to fetch the full resource. Using the above messages example, your app could fetch the complete message object along with the text by doing an authenticated (via your Bearer Token) GET request to `/messages/{id}` as shown below:

`GET https://webexapis.com/v1/messages/Y2lzY29zcGFyazovL3VzL01FU1NBR0UvMzIzZWUyZjAtOWFhZC0xMWU1LTg1YmYtMWRhZjhkNDJlZjlj`

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvMzIzZWUyZjAtOWFhZC0xMWU1LTg1YmYtMWRhZjhkNDJlZjlj",
  "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
  "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
  "personEmail": "matt@example.com",
  "text": "Something interesting and potentially sensitive",
  "created": "2015-12-04T17:33:56.767Z"
}
```

<a id="authenticating-requests"></a>
