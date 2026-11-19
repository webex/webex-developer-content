---
type: Guide
title: Events & Archiving
display_title: Events & Archiving
canonical_url: https://developer.webex.com/docs/compliance-events
content_type: documentation
product_group:
- webex-suite
categories:
- compliance
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/compliance-events)

Use the Events API to monitor and archive activity across your Webex organization. Learn which events are available and how to retrieve created and deleted messages and files.

## Events

### Introduction

The [Events API](https://developer.webex.com/docs/api/v1/events) endpoint gives developers access to events happening within their Webex organization. Events can be integrated with Data Loss Prevention (DLP) and CASB software to check for policy violations and to take action to resolve any issues. The events available for monitoring include activities such as posting messages, sending content such as files, and group space membership changes. The Events API endpoint can be integrated with your existing archiving software to archive an unlimited amount of Webex data. For access to events older than 90 days, the organization will need the [Pro Pack](https://www.cisco.com/go/pro-pack) for Webex Control Hub.

Use the Events API endpoint to access activities after they have occurred. Perhaps you need to replay every message sent to a room to comply with a legal audit process, or you need to know which rooms someone joined and left. The Events API endpoint will give you access to this information quickly and securely. In addition Webex provides a tool to uncover actions of a specific user in form of the eDiscovery report, available through the Webex Control Hub.

Known Limitations:
Membership events generated as a result of a POST to [/team/memberships](https://developer.webex.com/docs/api/v1/team-memberships/create-a-team-membership) do not currently contain a "roomType" or "isHidden" parameter.

Most events apply to an API resource of the same name. For example when a user creates a message a message creation event will be available. Some events though are not quite as straightforward to correlate. These include

- `Attachment Actions` events, which are part of Buttons&Cards and corresponding message creations.
- `Space Classifications`, which are Room Classifications (the `rooms` resource). The only supported event is `updated`.
- `File Downloads`, that get triggered whenever a user downloads a file.
- `File Transcodings` events, which are created when a user sees a preview of a file in their Webex client (title page).
- `Call Records(CDR)` events, which are created when a Webex Calling user makes or receives calls.
- `Business Texts(SMS)` events, which are created when a Webex Calling users sends or receives SMS messages.



| Resource                                               | created | updated | deleted | ended | read |
|--------------------------------------------------------|---------|---------|---------|-------|-------|
| [Attachment Actions](https://developer.webex.com/docs/api/v1/attachment-actions)  | X       |         |         |       |         |
| [Messages](https://developer.webex.com/docs/api/v1/messages)                      | X       | X       | X       |       |         |
| [Memberships](https://developer.webex.com/docs/api/v1/memberships)                | X       | X       | X       |       |         |
| [Space Classifications (rooms)](https://developer.webex.com/docs/api/v1/space-classifications)   |        | X       |         |       |         |
| [File Downloads](https://developer.webex.com/docs/api/v1/messages)  |        |         |         |       | X        |
| [File Previews a.k.a. File Transcodings](https://developer.webex.com/docs/api/v1/messages)  |        |         |         |       |  X       |
| [Room Tabs](https://developer.webex.com/docs/api/v1/room-tabs)  | X       |X         |X         |       |
| [Meetings](https://developer.webex.com/docs/api/v1/meetings)   |        |        |         |       X|
| [Meeting transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts)   |X        |       |         |       |
| [Meeting messages](https://developer.webex.com/docs/api/v1/meeting-messages)     |  X      | X       | X       |      |         |
| Call Records(CDR)     |  X      |        |        |      |         |
| Business Texts(SMS)     |  X      |        |        |      |         |

### Authorization Scopes

One scope for Events is available. Note that in order to use a `spark-compliance` scope you will need to be a designated compliance officer for your organization in Webex Control Hub. For instructions on how to add these scopes to your app and for a full list of all available authorization scopes see the [Integrations/OAuth Guide](https://developer.webex.com/docs/integrations).



Scopes: `spark-compliance:events_read`.



### Using Events

With the [Events API](https://developer.webex.com/docs/api/v1/events) endpoint you can retrieve information about user activities in Webex such as message activity in spaces, content or files shared, or user membership changes in spaces.

The `spark-compliance:events_read` scope can be used by compliance officers to retrieve events for the entire organization.

Each event contains a `data` object which mimics the Webex REST API resource (such as a message or membership) at the time the event took place. If properties are added to existing API resources, new events will include them; past events will not be updated to include the new properties.

When requesting a list of events from the API, the result may be split into pages. See the [Pagination](https://developer.webex.com/docs/api/basics#pagination) guide to learn how to navigate through paged API responses.

### Example: Retrieve Created Messages

To retrieve all messages that have been created, use the [List Events](https://developer.webex.com/docs/api/v1/events/list-events) endpoint. Use URL query parameters to limit the response to include only events related to the *messages* resource and only *created* items by using: `resource=messages&type=created`.

GET `https://webexapis.com/v1/events?resource=messages&type=created`

The attachment `content` object is shortened to `{}` in this example.

```json
{
  "items": [ {
    "id": "Y2lzY29zcGFyazovL3VzL0VWRU5UL2JiY2ViMWFkLTQzZjEtM2I1OC05MTQ3LWYxNGJiMGM0ZDE1NAo",
    "resource": "messages",
    "type": "created",
    "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
    "orgId": "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
    "appId": "null",
    "created": "2015-10-18T14:26:16+00:00",
    "data": {
      "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvOTJkYjNiZTAtNDNiZC0xMWU2LThhZTktZGQ1YjNkZmM1NjVk",
      "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
      "roomType": "group",
      "text": "PROJECT UPDATE - A new project plan has been published on Box: http://box.com/s/lf5vj. The PM for this project is Mike C. and the Engineering Manager is Jane W.",
      "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
      "personEmail": "matt@example.com",
      "attachments": [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": {}
        }
      ],
      "created": "2015-10-18T14:26:16+00:00"
    }
  } ]
}
```

In this example response, only one record is returned, but let’s take a look at it in detail. The next excerpt omits the `data` fields for brevity.

```json
{
  "items": [ {
    "id": "Y2lzY29zcGFyazovL3VzL0VWRU5UL2JiY2ViMWFkLTQzZjEtM2I1OC05MTQ3LWYxNGJiMGM0ZDE1NAo",
    "resource": "messages",
    "type": "created",
    "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
    "orgId": "OTZhYmMyYWEtM2RjYy0xMWU1LWExNTItZmUzNDgxOWNkYzlh",
    "appId": "null",
    "created": "2015-10-18T14:26:16+00:00",
    "data": {}
  } ]
}
```

The event object returned contains several fields which describe the event. This includes:

- `id`—a unique ID for the event
- `resource`—which resource the event includes
- `type`—the type of action which took place, such as created or deleted
- `actorId`—the ID of the person which committed the activity for this event
- `orgId`—the ID of the organization for the actor
- `appId`—the ID of the integration or bot which committed the activity for this event
- `created`—when the event took place
- `data`—the data for the event

The next excerpt focuses on the event's `data` object and omits other event fields. Its attachment `content` object is shortened to `{}`.

```json
{
  "items": [ {
    "data": {
      "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvOTJkYjNiZTAtNDNiZC0xMWU2LThhZTktZGQ1YjNkZmM1NjVk",
      "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vYmJjZWIxYWQtNDNmMS0zYjU4LTkxNDctZjE0YmIwYzRkMTU0",
      "roomType": "group",
      "text": "PROJECT UPDATE - A new project plan has been published on Box: http://box.com/s/lf5vj. The PM for this project is Mike C. and the Engineering Manager is Jane W.",
      "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9mNWIzNjE4Ny1jOGRkLTQ3MjctOGIyZi1mOWM0NDdmMjkwNDY",
      "personEmail": "matt@example.com",
      "attachments": [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": {}
        }
      ],
      "created": "2015-10-18T14:26:16+00:00"
    }
  } ]
}
```

Inside of the event object, the `data` object contains an object which represents the Webex REST API resource at the time the event took place. For instance, in this event, a message object represents a message at the time of its creation.

### Example: Retrieve Deleted Messages and Files

To retrieve all messages that have been deleted, use the List Events endpoint. Use URL query parameters to limit the response to include only events related to the messages resource and only deleted items by using: resource=messages&type=deleted.

Deleted messages have a reference back to the original message. Here is an example response for a single message that was deleted.

```json
 {
      "id": "Y2lzY29zcGFyazovL3VzL0VWRU5UL2MyZjhlMjYwLTgyYmUtMTFlYi1iYzdhLWNmZmIwNDA0Y2Y1YQ",
      "resource": "messages",
      "type": "deleted",
      "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS82ZDg4MDc3MS05MTA4LTRiMzktYmJlOS02OWJiNjA2ODBmZTG",
      "created": "2021-03-11T23:08:59.142Z",
      "data": {
        "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvNDYyMDQ4NTAtODJiZS0xMWViLWJkYmUtM2IyYWMxNWZlNjg5",
        "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vMGQ5MTg1ZDAtODJiZS0xMWViLWEyNGYtZDMxMWQ2NmMwNjBj",
        "roomType": "group",
        "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS82ZDg4MDc3MS05MTA4LTRiMzktYmJlOS02OWJiNjA2ODBmZTG",
        "personEmail": "example@gmail.com"
      }
 }
```

For a Compliance Officer, it is important to understand what has been deleted. The way to go about it, is to use the message ID and query the /messages resource with it. Both the text and in this case file attachment are returned.

GET `https://webexapis.com/v1/messages/Y2lzY29zcGFyazovL3VzL01FU1NBR0UvNDYyMDQ4NTAtODJiZS0xMWViLWJkYmUtM2IyYWMxNWZlNjg5 `


The sample response looks like this

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL01FU1NBR0UvNDYyMDQ4NTAtODJiZS0xMWViLWJkYmUtM2IyYWMxNWZlNjg5",
  "roomId": "Y2lzY29zcGFyazovL3VzL1JPT00vMGQ5MTg1ZDAtODJiZS0xMWViLWEyNGYtZDMxMWQ2NmMwNjBj",
  "roomType": "group",
  "text": "check this",
  "files": [
    "https://integration.webexapis.com/v1/contents/Y2lzY29zcGFyazovL3VzL0NPTlRFTlQvNDYyMDQ4NTAtODJiZS0xMWViLWJkYmUtM2IyYWMxNWZlNjg5LzA"
  ],
  "personId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS82ZDg4MDc3MS05MTA4LTRiMzktYmJlOS02OWJiNjA2ODBmZTG",
  "personEmail": "example@gmail.com",
  "html": "<p>check this</p>",
  "created": "2021-03-11T23:05:29.685Z"
}
```

The deleted message had a file attachment. Any file attachment is always encapsulated into a message, even if the user did not supply any text. For the Compliance Officer to check the file that was deleted, they have to query the /contents URL. Only the Compliance Officer will have access to the file and only for the duration of the default retention period. Regular users and after the retention period the query will return a http `404`.
If the Compliance Officer tries to delete the message again they will receive a `410` error status, which should be avoided.

For more information about how to use the Events API endpoint, please see the [Events API Reference](https://developer.webex.com/docs/api/v1/events).
