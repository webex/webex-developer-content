---
type: Article
title: Calling APIs Overview
canonical_url: https://developer.webex.com/blog/calling-apis-overview
content_type: blog
date: '2022-10-31'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/calling-apis-overview)

[Webex Calling](https://www.webex.com/cloud-calling.html) is a cloud-based phone system that contains a comprehensive set of business calling and PBX functionality right out of the box. With customizable plan options and a high level of security, Webex Cloud Calling decreases the cost and difficulty of administering an on-premises phone system. The [Webex Calling platform](https://developer.webex.com/docs/webex-calling) also provide developers an assortment of APIs to automate and extend functionality for administrator provisioning, end-user call controls, generating reports and more.

To get a better lay of the land, let’s take a high-level look at what APIs are available for each area of Webex Calling and how they can be leveraged to power some great integration applications.

### Calling APIs for Administrator Integrations

The first group of Calling APIs we’ll focus on are exclusively for [Webex Administrators](https://developer.webex.com/docs/admin), to extend Control Hub functionality for user provisioning and call reports. When testing these endpoints, pay close attention that the correct admin-level scopes are configured, as noted in the linked API documentation below.  

#### Provisioning APIs

The Webex Calling APIs can automate all the bulk provisioning tasks needed to deliver solutions reliably and efficiently. These provisioning tools can be leveraged to create Webex Calling integrations that automates the creation and management of users and locations, as well as the configuration of custom organizational settings. Let’s take a closer look at the provisioning-specific APIs for Webex Calling administrators.

- [People API](https://developer.webex.com/docs/api/v1/people): In this context, ‘people’ refers to registered users of Webex. These endpoints allow the creation and management of users in a Webex organization. To do this within the context of Webex Calling, administrators need to specify the `callingData` parameter as `true` in their API calls.
- [Locations API](https://developer.webex.com/docs/api/v1/locations): These *read-only* endpoints are used to organize Webex Calling features within physical locations, configured within Control Hub. The responses essentially provide name and mailing address data for the location. 
- [Organization Settings API](https://developer.webex.com/docs/api/v1/ucm-profile): This powerful set of endpoints support reading and writing of Webex Calling settings for a specific organization, including call routing &amp; forwarding, hunt groups, dial plans, route lists &amp; groups, phone numbers, paging groups, auto attendants, and more.
- [Calling Person Settings API](https://developer.webex.com/docs/api/v1/user-call-settings): Settings for individual users are configured and managed within this grouping of APIs, similar to the organization-specific ones mentioned above. These settings include calling behaviors, privacy, permissions, barge-ins, intercepts, recordings, caller ID, DND, schedules, call waiting, and more.
- [Workplace Settings with Numbers API](https://developer.webex.com/docs/api/v1/workspace-call-settings-with-numbers): Workspaces in Webex represent physical rooms inside organizational locations, like conference rooms, meeting spaces, lobbies, and lunchrooms. This is a read-only endpoint for Webex Calling, to retrieve a list of phone numbers assigned to a particular workspace. 

For more efficiency, developers can also utilize the [Provisioning SDK](https://github.com/jeokrohn/wxc_sdk) to further streamline these API methods. Check out the helpful [SDK documentation](https://wxc-sdk.readthedocs.io/en/latest/) to learn more.

#### Webex Calling Report APIs

Reports help you track and analyze the performance of Webex services in your organization. You can use these reports to see details for each meeting, how often users are messaging each other, details for Webex Calling calls and call queues, how often Webex devices are used, onboarding information, and more. These reports are generated through templates that are managed [in Control Hub](https://callinghelp.webex.com/calling-admin-portal-reports/). The [Webex Calling report templates](https://help.webex.com/en-us/article/nmug598/Reports-for-Your-Cloud-Collaboration-Portfolio#Cisco_Concept.dita_6136cd51-f6a4-427f-9da9-0cfb89be6330) can generate reports for call quality, engagement, and historical details. These templates can also be used to produce and download reports via the Webex API.  A great example integration that utilizes these APIs can be found on the Webex App Hub– [Microcall CDR Reporting](https://apphub.webex.com/applications/microcall-cdr-reporting-micro-tel-inc). They use the information in the call detail records (CDRs) to populate information in management dashboards.

It’s also worth noting that this group of APIs are in the process of being updated and expanded, with many new enhancements on the way, so stay tuned for future announcements. However, developers can still leverage the following APIs today to generate reports automatically and synchronize with their workflows.

- [Report Templates API](https://developer.webex.com/docs/api/v1/report-templates/list-report-templates): This is a single, *read-only* API to list all the available report templates (Calling included) that can be generated. 
- [Reports API](https://developer.webex.com/docs/api/v1/reports): This set of APIs allows the creation and management of reports that are generated through the report templates that are configured in an organization.

Do note, developers can obtain a licensed Webex organization to test the Provisioning and Calling Reports APIs (as an administrator), by requesting a [Webex Developer Sandbox](https://developer.webex.com/blog/developer-sandbox-now-available). The sandbox provides administrator access to a test Webex organization that is managed through Control Hub. Once the sandbox is all setup, this [help desk article](https://help.webex.com/en-us/article/njvdjf2/Configure-Webex-Calling-for-your-organization) provides insight into how Webex Calling is configured in an organization.

### Calling APIs for End User Actions

Outside of administration, there are also Webex Calling APIs for end-user actions, like real-time telephony controls and voice messaging.  Keep in mind, integrations that use these APIs will require a different set of user scopes that are separate from the administrator level. These APIs also have a great [Postman collection](https://github.com/webex/postman-webex-calling) to give developers a head start.

#### Call Control APIs

[Call Controls](https://developer.webex.com/docs/api/v1/call-controls) can be used to perform calling actions and provide information about active calls in 3<sup>rd</sup> party applications. These can be used to integrate a custom call interface or automate other in-call workflows. There are a broad list of intuitive calling control APIs available, such as [dial](https://developer.webex.com/docs/api/v1/call-controls/dial), [answer](https://developer.webex.com/docs/api/v1/call-controls/answer), [hangup](https://developer.webex.com/docs/api/v1/call-controls/hangup), [transfer](https://developer.webex.com/docs/api/v1/call-controls/transfer), and [start](https://developer.webex.com/docs/api/v1/call-controls/start-recording)/[stop recording](https://developer.webex.com/docs/api/v1/call-controls/stop-recording) for initiating and managing active calls. Additionally, read-only endpoints for listing past [calls](https://developer.webex.com/docs/api/v1/call-controls/list-calls), [details](https://developer.webex.com/docs/api/v1/call-controls/get-call-details), and [history](https://developer.webex.com/docs/api/v1/call-controls/list-call-history) are provided. These conceivably can be used to populate data in 3<sup>rd</sup> party widgets, dashboards, CRMs and more.

A good example integration that leverages these end-user Calling APIs is the aptly named– [Call Control](https://apphub.webex.com/applications/call-control-call-control-llc), which is listed on the Webex App Hub. This integration utilizes these Control APIs to block unwanted calls and spammers, helping teams stay more productive. 

#### Voice Messaging APIs

Webex Calling includes Voice Messaging services, which can be controlled and managed via user-level [REST APIs](https://developer.webex.com/docs/api/v1/user-call-settings).  These actions include [list messages](https://developer.webex.com/docs/api/v1/user-call-settings/list-messages), [delete message](https://developer.webex.com/docs/api/v1/user-call-settings/delete-message), [mark as read](https://developer.webex.com/docs/api/v1/user-call-settings/mark-as-read)/[unread](https://developer.webex.com/docs/api/v1/user-call-settings/mark-as-unread), and [get messages summary](https://developer.webex.com/docs/api/v1/user-call-settings/get-message-summary), making it possible for developers to create a custom voicemail interface in a very streamlined way.

### Calling Events (Webhooks)

The Webex Calling platform also provides user level webhooks to notify integrations of changes in call status, such as answered, disconnected, forwarded, resumed, recording stop/start, and more.  The JSON payload for call event webhooks contain a variety of retrievable data that can be acted on. For reference, a webhook for a disconnected call would return something like this example JSON payload:

```javascript
 {
    "id": "Y21zY29zcGFyazovL3VzL1",
    "name": "Ni0xMWVILTKYTYEM5YTUZ...",
    "targetUrl": "https://example.com/calls/",
    "resource": "telephony_calls",
    "event": "deleted",
    "orgId": "OWM5LTRINWQtYjZiOCO5NDZ3MGI...",
    "createdBy": "YzOC1jODQwLTMmU...",
    "appId": "Y21zY29zcGFyazovLY...",
    "ownedBy": "creator",
    "status": "active",
    "created": "2022-09-14T18:03:25.829Z",
    "actorId": "Y21zY29zcGFyazovL3VzL1...",
    "data ": {
        "eventType": "disconnected",
        "actorPersonId": "RS84MWNhZjUzOC1j...",
        "orgId": "OWM5LTRINWQtYjZiOCO5NDZ3MGI...",
        "eventTimestamp": "2022-10-15T18:06:20.7817",
        "callId": "Y21zY29zcGFyazovL3Vz...",
        "call SessionId": "OGQ3YzhkNzgtZjIxZib...",
        "personality": "terminator",
        "state": "disconnected",
        "remoteParty": {
            "name": "agent x",
            "number": "1012",
            "personId": "Y21zY29zcGFyazovL3V...",
            "privacyEnabled": false,
            "callType": "location"
        },
        "created": "2022-09-15T18:06:10.2692",
        "answered": "2022-09-15T18:06:17.2117",
        "disconnected": "2022-9-15T18:06:20.781Z"
    }
}
 
```

### Note about Webex for Cisco Broadworks APIs

Another set of APIs found under the Calling banner is [Webex for BroadWorks](https://developer.webex.com/docs/webex-for-broadworks-developers-guide). In a nutshell, [BroadWorks](https://www.cisco.com/c/en/us/products/unified-communications/webex-broadworks/index.html) is a call control system and VoIP application server hosted by Service Providers (SP).  An SP can wrap Broadworks up with other telephony services (PSTN, ordering, billing, support, etc.) to offer to a complete solution to their end customers. BroadWorks is also the core call control system for [Cisco BroadCloud](https://www.cisco.com/c/en/us/solutions/collaboration/broadcloud-calling/index.html) and is similar to [Cisco HCS](https://www.cisco.com/c/en/us/solutions/collaboration/hosted-collaboration-solution/index.html), in the sense that it's a partner hosted platform.

The Broadworks platform has APIs that are distinct from the Webex Calling APIs. Any endpoints that are noted as BroadWorks, such as [BW Billing Reports](https://developer.webex.com/docs/api/v1/broadworks-billing-reports), [BW Workspaces](https://developer.webex.com/docs/api/v1/broadworks-workspaces), [BW Enterprises](https://developer.webex.com/docs/api/v1/broadworks-enterprises), and [BW Subscribers](https://developer.webex.com/docs/api/v1/broadworks-subscribers), are exclusively for those Service Providers that partner with the BW service.

### Need Any Help?

Don’t forget that the [Webex Developer Support Team](https://developer.webex.com/support) is standing by to assist. On top of that, anyone can ask a question, start a conversation, or join an existing discussion on the Webex for [Developers Community Forum](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers). We can also be reached on Twitter via [@WebexDevs](https://twitter.com/WebexDevs) for questions or feedback.
