---
type: Article
title: Exploring the Webex Calling Reports and Analytics APIs
canonical_url: https://developer.webex.com/blog/exploring-the-webex-calling-reports-and-analytics-apis
content_type: blog
date: '2024-04-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/exploring-the-webex-calling-reports-and-analytics-apis)

[Webex Calling](https://www.webex.com/suite/enterprise-cloud-calling.html) is an enterprise-grade, cloud phone system with a full range of features for businesses of all sizes. The Webex Calling platform also offers a wide set of APIs for building powerful integrations that extend and enhance out-of-the-box functionality. These integrations can automate bulk operations, real-time call actions, and other tasks that run on a long-term basis, which makes them particularly useful for large enterprises and service providers.

The Webex Calling APIs fall into three fundamental categories that correlate with the stages of phone call interactions - pre-call setup, in-call management, and post-call analysis. First, the [Provisioning APIs](https://developer.webex.com/docs/webex-calling-provisioning-apis) that manage initial calling configurations and onboarding before calls are made. These are mainly administrator-level functions that are otherwise done manually, one at a time in Control Hub. The second category contains the [Call Control APIs](https://developer.webex.com/blog/webex-calling-getting-started-with-call-control-apis), for managing real-time actions during calls and furnishing data on current and past calls. This article will concentrate on the third category, which is for managing post-call processes with the **Reports &amp; Analytics APIs**. We will explore how integrations can leverage both the Reports APIs to generate and retrieve comprehensive call reports for a Webex Calling organization, and the Detailed Call History API to efficiently gather detailed historical call information.

To get a better idea of what kind of integrations can be built with these APIs, there are some great examples listed in the [Webex App Hub](https://apphub.webex.com/). One of these integrations is from our partner, [Imagicle](https://apphub.webex.com/applications/imagicle-call-analytics-imagicle). Their app utilizes the APIs in intuitive ways to extend the standard Webex report tools with over 50 different reports that analyze telephone traffic, costs, and customer service performances. Another reporting integration is from our partner, [Microcall](https://apphub.webex.com/applications/microcall-cdr-reporting-micro-tel-inc). Their app gathers call detail records (CDRs) to power dashboards for managers, to help them maintain their voice infrastructure and make data-driven decisions.

### Report Templates

There are a variety of [Webex Calling report templates](https://help.webex.com/en-us/article/nmug598/Reports-for-Your-Cloud-Collaboration-Portfolio#Cisco_Concept.dita_6136cd51-f6a4-427f-9da9-0cfb89be6330) available for administrators to configure inside Control Hub. Once they are setup in Control Hub, these templates can be used by integrations to create reports via the [Webex Reports API](https://developer.webex.com/docs/api/v1/reports), which is available for organizations with [Pro Pack for Cisco Webex](https://www.cisco.com/go/pro-pack). To get familiarized with how report templates work in Control Hub, check out this [help article](https://help.webex.com/en-us/article/nmug598/Reports-for-Your-Cloud-Collaboration-Portfolio) first.

Each report template contains different types of Webex Calling data to track several kinds of statistical details. The data included in these reports are generated the following day, which can be up to 24 hours after a call has completed. The standard report templates for Webex Calling are as follows:

- **Detailed Call History Report** – contains a comprehensive log of call information, such as timestamps, call duration, call status, and the identities of both the initiator and receiver of the calls, that can be used to view high-level trends or inspect specific call types. More information about the Call History Report can be found in the [support docs](https://www.cisco.com/c/en/us/support/docs/unified-communications/webex-calling/220377-understand-detailed-call-history-report.html).
- **Calling Media Quality Report** - contains metrics for media quality of calls, such as latency, jitter, and packet loss for each call leg that had an established Webex Calling media session. This report can be leveraged to monitor and assess the quality of voice and video calls within an organization to improve the user experience.
- **Calling Engagement Report** - provides insights into how users in an organization are utilizing the Webex Calling system, including valuable metrics such as call volume, usage patterns, and adoption rates over time. This is used to better understand the ways employees are interacting with the system, identify trends in calling behavior, and evaluate the effectiveness of the tools provided.
- **Calling Quality Report** - contains quality metrics for calls made or received by users specifically within the Webex Calling app, such as jitter, latency, and packet loss. This helps administrators to better pinpoint and troubleshoot quality issues on the client side.
- **Call Queue Stats Report** – provides details of call queues that have been set up in an organization, such as the number of incoming calls, wait times, call abandonment rates, and the efficiency of call handling by agents. This report can be instrumental for managers to assess how well their call queues are operating and identify areas for improvement.
- **Call Queue agent stats report** – provides detailed analysis of all the agents that have been assigned to call queues in an organization, to get insight on an agent’s number of calls handled, average handle time, and service level achievements. Supervisors can utilize this report to monitor and optimize agent productivity, assess workload distribution, and ensure that customer service objectives are met.
- **Auto-attendant stats summary** – details statistics of calls routed to auto-attendants in an organization, such as the volume of calls received, the number of calls handled by the auto-attendant, and caller selections within the menu. This data helps administrators understand how effective the auto-attendant is at managing incoming calls and identify any changes that might be needed to improve caller experience and call routing efficiency.
- **Auto-attendant business &amp; after-hours key details** – contains information about calls routed to auto-attendants during specified business and after-hours periods. This report breaks down the interaction patterns of callers with the auto-attendant, showing which menu options are selected during different times of the day. This can help administrators discern call distribution and caller behavior during office hours versus after-hours, enabling them to tailor the auto-attendant system for improved efficiency and customer service.

For organizations that want to tailor their reports with specific data, [custom templates](https://help.webex.com/en-us/article/nmug598/Reports-for-Your-Cloud-Collaboration-Portfolio#reference_rs5_z52_nsb) can also be configured and setup inside Control Hub.

### Traversing the Reports APIs

Once the templates are in order, the APIs can be leveraged to create a report. To work with the Reports APIs, an administrator-level integration with the `analytics:read_all` scope will be required. For more information on getting started with the Reports API, check out the [administrator developer guide](https://developer.webex.com/docs/admin#reports-api).

Generally, the first endpoint used in a workflow is the [List Report Templates API](https://developer.webex.com/docs/api/v1/report-templates), for retrieving all the templates from the administrator’s organization. An example JSON response from this API will look something like this:

```json
{    "items" :
        [
            {
                "Id" : 130,
                "title" : "Agent Activity",
                "service" : "Calling",
                "maxDays" : 31,
                "identifier" : "queueStats",
                "validations" :
                    [
                        {
                            "field" : "templateId",
                            "required" : "yes"
                        }
                    ]
            }
        ],
    "numberOfTemplate" : 1
}
```

Each template listed in the response body has a unique ID value that is used in subsequent API calls for creating and managing reports.

Next in this workflow, the [Create a Report API](https://developer.webex.com/docs/api/v1/reports/create-a-report) is used to generate a new report from a chosen template. The `templateId` retrieved in the last API call is the only required parameter for this endpoint. A `startDate` and/or `endDate` can also be optionally included, to specify the range of the report.

In this example, the process is initiated with an API call to `/v1/reports` with the following content:

```json
{
  "templateId": 130,
  "startDate": "2024-02-01",
  "endDate": "2024-02-05"
}
```

The new report gets created and the response body will look something like this:

```json
{
    "items":
        {
            "id": "YWE0MzFmZWM0ZmE"
        }
}
```

Be sure to make note of the report `id` that is included in the response, which is needed in the next step to check the status of the report and get the download URL. 

While the report is being generated, the `status` can be checked with the [Get Report Details API](https://developer.webex.com/docs/api/v1/reports/get-report-details), using the ID you noted in the previous step. An example response can look like this:

```json
{
  "id": "YWE0MzFmZWM0ZmE",
  "title": "Agent Activity",
  "service": "Calling",
  "startDate": "2020-02-01",
  "endDate": "2020-02-05",
  "siteList": "calling.example.com",
  "created": "2024-04-01 17:13:39",
  "createdBy": "Yzf6GbAmQMD0YeB",
  "scheduledFrom": "API",
  "status": "done",
  "downloadURL": https://downloadservicebts.webex.com/api?reportId=YWE0MzFmZWM0ZmE
}
```

In this example, the report `status` is `done` and a link is provided in the `downloadURL` property that can be used to retrieve the report. If the report is still in the process of being generated, the `status` will indicate `"In progress"`.

Each report can be downloaded up to 30 times and organizations may keep up to 50 reports at any time. After creating and downloading a report, it should be then deleted to make room for the next report using the [Delete a Report API](https://developer.webex.com/docs/api/v1/reports/delete-a-report). This endpoint only needs the `reportID` value to delete a report. When a deletion is successful, the API returns a `200`-response code.

### Webex Detailed Call History API

For scenarios that require quicker retrieval of call detail records, perhaps before the Webex-generated reports are compiled the next day, there is another API available. The [Webex Detailed Call History API](https://developer.webex.com/docs/api/v1/reports-detailed-call-history) provides a more expedient, programmatic way to retrieve **call detail records** (CDRs) for calls completed from 48 hours to as recent as 5 minutes ago.

The first step to start using the Webex Detailed Call History API is to enable user access in the “Administrator roles” section of Webex Control Hub, as shown here:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc5fcb98857c2174d/webex-calling---reports-analytics-apis-2.png)

Once the API access is granted in Control Hub, integrations will just need to enable the `spark-admin:calling_cdr_read` and the `spark-admin:locations_read` scopes to start using the API.

While the Detailed Call History API works much like the other Webex APIs, the endpoint has a unique “analytics” URL: `analytics.webexapis.com/v1/cdr_feed`.

There are four query parameters accepted here: `startTime` (required), `endTime` (required), `locations` (optional filter by locations within an organization), and `max` (optional number of results per page). The Detailed Call History API returns the CDRs in JSON format, providing over 50 points of data. This example response body shows the data that can be obtained from a Webex Calling CDR:

```json
  "items": [
    {
      "Answer indicator": "Yes",
      "Answer time": "2024-03-14T11:01:17.551Z",
      "Answered": "true",
      "Authorization code": "107",
      "Call ID": "SSE1101163211405201218829100@10.177.4.29",
      "Call outcome": "Success"
      "Call outcome reason": "Normal",
      "Call transfer Time": "2024-03-14T18:21:29.707Z",
      "Call type": "SIP_ENTERPRISE",
      "Called line ID": "CALLEDCLIDGOESHERE",
      "Called number": "2002",
      "Calling line ID": "YOURCLIDGOESHERE",
      "Calling number": "2001",
      "Client type": "SIP_TOLLFREE",
      "Client version": "1.0.2.3",
      "Correlation ID": "8e8e1dc7-4f25-4595-b9c7-26237f824535",
      "Department ID": "4370c763-81ec-403b-aba3-626a7b1cf264",
      "Device MAC": "6C710D8ABC10",
      "Dialed digits": "1246",
      "Direction": "ORIGINATING",
      "Duration": 36,
      "Final local SessionID": "82bb753300105000a0000242be131609",
      "Final remote SessionID": "cfe67b8a00105000a0000242be131609",
      "Inbound trunk": "InTrunk",
      "International country": "US",
      "Local call ID": "113104021:0",
      "Local SessionID": "82bb753300105000a0000242be131609",
      "Location": "Richardson",
      "Model": "8851-3PCC",
      "Network call ID": "BW2356451711108231501755806@10.21.0.192",
      "Org UUID": "408806bc-a013-4a4b-9a24-85e374912102",
      "Original reason": "UserBusy",
      "OS type": "na",
      "Outbound trunk": "OutTrunk",
      "Release time": "2023-10-12 21:22:32.621",
      "Ring duration": 23,
      "Redirect reason": "Unavailable",
      "Redirecting number": "+13343822691",
      "Related call ID": "760583469:0",
      "Related reason": "CallQueue",
      "Releasing party": "Remote",
      "Remote call ID": "113103977:0",
      "Remote SessionID": "6bf2f47800105000a0000242be13160a",
      "Report ID": "0a0c2eb7-f1f6-3326-86f9-565d2e11553d",
      "Report time": "2020-05-14T11:01:52.723Z",
      "Route group": "RouteGrpAA",
      "Site main number": "+14692281000",
      "Site timezone": "-300",
      "Site UUID": "474d4f70-4ef5-4d52-9e1d-b207086629e0",
      "Start time": "2020-05-14T11:01:16.545Z",
      "Sub client type": "MOBILE_NETWORK",
      "Transfer related call ID": "2340586843:0A",
      "User": "John Andersen",
      "User number": "+81546668399",
      "User type": "User",
      "User UUID": "47f0d0c2-f05a-44cc-870d-7a3daf859c6c"
    }
  ]
}
```

This call data can then be used to build custom reporting integrations, power management dashboards, and more. For detailed information and a demo on how to use the Detailed Called History API, see this [helpful blog post](https://developer.webex.com/blog/webex-detailed-call-history-api) by Collaboration Technical Solutions Architect, Justin Haefner.

### Have Any Questions? Ask Us!

There was a lot of information covered here and naturally, questions may arise. The good news? Our [Webex Developer Support Team](https://developer.webex.com/support) is standing by, ready and happy to assist. Alternatively, feel free to join or kick off a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
