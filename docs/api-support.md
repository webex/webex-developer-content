---
type: Guide
title: Notes on API Support
display_title: Notes on API Support
canonical_url: https://developer.webex.com/docs/api-support
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/api-support)

The following tables describe the exceptions to API support in the Webex REST APIs as well as the supported legacy XML APIs.

## REST APIs

There are exceptions to the availability of Webex REST APIs documented in this portal:



| **API REST Endpoint** | **Link to Developer Portal** | **FedRAMP** |
| --- | --- | --- |
| broadworks/enterprises | [https://developer.webex.com/docs/api/v1/broadworks-enterprises](https://developer.webex.com/docs/api/v1/broadworks-enterprises) | NO |
| broadworks/subscribers | [https://developer.webex.com/docs/api/v1/broadworks-subscribers](https://developer.webex.com/docs/api/v1/broadworks-subscribers) | NO |
| meetingTranscripts | [https://developer.webex.com/docs/api/v1/meeting-transcripts](https://developer.webex.com/docs/api/v1/meeting-transcripts) | NO |
| people | [https://developer.webex.com/docs/api/v1/user-call-settings](https://developer.webex.com/docs/api/v1/user-call-settings) | NO |
| telephony/calls | [https://developer.webex.com/docs/api/v1/call-controls](https://developer.webex.com/docs/api/v1/call-controls) | NO |
| telephony/config/locations | [https://developer.webex.com/docs/api/v1/ucm-profile](https://developer.webex.com/docs/api/v1/ucm-profile) | NO |
| webhooks | [https://developer.webex.com/docs/api/v1/webhooks](https://developer.webex.com/docs/api/v1/webhooks) | YES<sup>1</sup>|

<sup>1</sup> The following resource types are not available for Webhooks: meetings, recordings, meetingParticipants, and meetingTranscripts.

## Legacy XML APIs

The XML APIs used to setup and control the meetings experience are available in their entirety in the FedRAMP environment:



| XML REST Endpoint | Link to Developer Portal | FedRAMP |
| --- | --- | --- |
| UserService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!overview/user-service | YES |
| GeneralSessionService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!general-session-service-overview | YES |
| MeetingServices | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!meeting-service-overview | YES |
| TrainingSessionService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!training-session-service-overview | YES |
| EventCenterSessions | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!event-center-sessions-overview | YES |
| SupportCenterService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!support-center-service-overview | YES |
| HistoryService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!history-service-overview | YES |
| SiteService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!site-service-overview | YES |
| Meeting AttendeeService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!meeting-attendee-service-overview | YES |
| MeetingTypeService | https://developer.cisco.com/docs/webex-xml-api-reference-guide/#!meeting-type-service-overview/webex-xml-api-meeting-type-service | YES |
