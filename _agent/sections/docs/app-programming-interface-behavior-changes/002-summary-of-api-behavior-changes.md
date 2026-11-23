---
type: Excerpt
canonical_url: https://developer.webex.com/docs/app-programming-interface-behavior-changes
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Summary of API Behavior Changes
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/app-programming-interface-behavior-changes). [Full Markdown](../../../../docs/app-programming-interface-behavior-changes.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This page highlights recent API behavior changes associated with the upgrade to the Webex Suite Meeting Platform.

---

Developers have reported unexpected changes in functionality, such as [join links](https://developer.webex.com/docs/api/v1/meetings/join-a-meeting) requiring authentication and the [meeting chats API](https://developer.webex.com/docs/api/v1/meeting-chats) not returning new results.

If you encounter any of these issues, open a ticket with our [support team](mailto:devsupport@webex.com) so we can validate your environment and recommend the best path forward.

These changes are a byproduct of the ongoing migration of customer sites to the Webex Suite Meeting Platform (WSMP).

## Selected section

## Summary of API Behavior Changes

### Availability of direct messages in the meetingMessages event
- _NEW_ `meetingMessages` in the /events API will soon also show direct messages (private conversations between meeting attendees) as well as messages exchanged in breakout sessions.

### Availability of Sli.do API for Poll and QA
- _NEW_ The Sli.do "Poll" and "QA" reports should be accessed via the Sli.do APIs. Documentation can be found for the [US](https://datapi-us1.slido.com/redoc) and [EU](https://datapi-eu1.slido.com/redoc) with different access points. A helpful [FAQ](https://developer.slido.com/help) is provided as well.

### Meeting join links will need authentication and do not allow host role assignment
- Joining a Webex Suite Meeting Platform meeting via the join link now requires explicit login credentials and does not allow for assigning a host role through the link.

### The Meetings Chat legacy API is replaced by the events API most commonly used by DLP/CASB vendors
- The meeting chat for compliance use cases can now be accessed through the [events API](https://developer.webex.com/docs/api/v1/events). The Webex Suite Meeting Platform leverages the robust Webex chat functionality, which provides enhanced features such as meeting sharing to spaces and pre- and post-meeting huddles. Compliance officers can access chat data via the [/events API](https://developer.webex.com/docs/api/v1/events), specifically the resource type `meetingMessages`. If necessary, unwanted meetingMessages can be removed using the [/meetingMessages API](https://developer.webex.com/docs/api/v1/meeting-messages). It's important to note that meetingMessages are ephemeral unless configured otherwise in Control Hub. We plan to introduce the ability to configure the persistence of direct messages (person-to-person) and breakout session messages. meetingMessage events are only created for meetings on the new WSMP platform. Historical messages in meetings are not carried over.

### Meetings in spaces must be explicitly licensed through a new scheduling API call
- Meetings in spaces work differently. When a space meeting is desired, a Webex Meeting must be [scheduled](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) with a `roomid`. Meetings are only loosely associated with spaces. This also means the [room meetings info](https://developer.webex.com/docs/api/v1/rooms/get-room-meeting-details) API will no longer work, and all meeting info should be collected from the [meetings](https://developer.webex.com/docs/api/v1/meetings) endpoint.

### Native QA and Poll is replaced by Sli.do functionality
- Native `polling` and `QA` are no longer available within meetings powered by the Webex Suite Meeting Platform. Instead, the Sli.do embedded app must be used for this purpose. As a result, the [meeting polls](https://developer.webex.com/docs/api/v1/meeting-polls) and [QA API](https://developer.webex.com/docs/api/v1/meeting-q-and-a) do not contain any data. To collect data about polls and QA, please open a TAC request for access.

### Certain meeting preconfigurations are not available any longer
- The `enabledAnnotate` field in the update or [create a meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting) API is not available for the Webex Meetings Suite. Other unavailable fields include:
`enabledAnnotate`, `enabledSaveDocument`, `enabledPrintDocument`, `enabledViewThumbnails`, `enabledRemoteControl`, `enabledViewAnyDocument`, `enabledViewAnyPage`, `enabledContactOperatorPrivately`, `enabledChatHost`, `enabledChatPresenter`, `enabledChatOtherParticipants`.

### A note about meeting transcripts when AI Assistant is enabled in the meeting
- The [meeting transcripts endpoints](https://developer.webex.com/docs/api/v1/meeting-transcripts) return transcripts for meetings where either Webex Assistant or Cisco AI Assistant is enabled.
