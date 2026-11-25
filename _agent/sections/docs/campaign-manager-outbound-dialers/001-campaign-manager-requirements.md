---
type: Excerpt
canonical_url: https://developer.webex.com/docs/campaign-manager-outbound-dialers
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Campaign Manager Requirements
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/campaign-manager-outbound-dialers). [Full Markdown](../../../../docs/campaign-manager-outbound-dialers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

A Campaign Manager (CM) is designed with the functionality and features to increase right party contacts and meet campaign objectives in an outbound environment by intelligently managing customer contacts as they move through the system. LCM enables contact centers to reach the right people at the right number to best meet campaign objectives.

---

An outbound campaign dialer is a tool used in call centers and telemarketing to automate the process of making outgoing calls to a list of contacts. The dialer helps increase efficiency, improve agent productivity, and optimize campaign performance. The Webex Contact Center Dialer using the Next Generation Media Platform (RTMS) supports the following types of pacing modes:

- **Progressive**
  - The dialer automatically dials a pre-defined number of contacts, one after another once an agent is available.
  - Calls are connected to agents in a sequential manner, ensuring that agents are available to handle each call.
- **Predictive**
  - Uses predictive algorithms to anticipate how many calls to dial when an agent becomes available.
  - Calls are dialed in anticipation of agent availability, aiming to minimize idle time and maximize the number of answered calls.
  - The dialer adjusts the dialing rate based on historical call data and agent performance.
- **IVR**
  - Can be run in either progressive or predictive mode.
  - Calls are dialed based on the configured dialing rate and on IVR port availability.
  - If run in predictive mode, the dialing rate is adjusted based on historical call data to maintain configured abandoned rate.
- **Preview**
  - The dialer presents a preview of the contact, with opted customer information, to the agent before dialing.
  - If the agent accepts the contact, the call is dialed and connected to the agent.
  - If the agent skips or removes the contact, an appropriate call disposition is sent to the Campaign Manager and a new contact is presented to the agent.
  - Can be run in either standard or direct preview mode.
    - In standard mode, CPA(Call Progress Analysis) can be performed to determine if the call was answered by a live customer or an answering machine.<br>
      Based on the CPA result, the dialer can connect the call to agent or send appropriate call disposition to the Campaign Manager.
    - In direct mode, CPA is not performed and the dialer directly connects the call to the agent.
  - The dialing rate can only be 1.0 in both preview modes.

## Selected section

## Campaign Manager Requirements

To bring your own Campaign Manager to Webex Contact Center you need to provide a resource domain, an authentication token and the dialing list.

### Resource Domain

A Campaign Manager resource domain is required which uses the following authentication type:
- Basic Authentication (Username/Password)

And must provide endpoints for

1.	Providing an authentication token. This is a URL that is at the ORG level to provide a token that will subsequently be passed by the dialer on future Campaign Manager requests for records.
2.	Fetching the dialing lists. This is a per Campaign URL that provides records to the dialer
3.	A webhook subscription. This is a per ORG URL that will receive the dispositions of the calls.

The resource domain will need to be configured as a custom connector in Webex Contact Center Control Hub.  The custom connector requires the Username, Password and URL needed to obtain the token.  See the section on Connecting to the Webex Contact Center below.


### Authentication Token

The Campaign Manager needs to provide a token.  All external API requests to the Campaign Manager will be authenticated using this token.  This includes requests to fetch the dialing list and to subscribe to call disposition events.

The token should have an expiry of 720 minutes and follow the JSON format shown below. WXCC will periodically request the token when it needs to be refreshed, and it will be provided in the header to the Campaign Manager.

```bash
{
    "Token": "<CAMPAIGN_MANAGER_ACCESS_TOKEN>",
   
    "ExpiresIn": 720
}
```

### Dialing List

The Campaign Manager needs to provide the list of contacts in the endpoint associated with the dialing lists. Once the records are retrieved by the dialer, They should not be returned in a subsequent request unless they are intended to be retried.

The dialer will periodically request the list using the unique dialing list fetch URL provided when the campaign was started, refer to the Start Campaign Request API section below.  The response to the dialer must be in the JSON format and contain the following fields as shown below.  Once the dialer gets a success response it starts dialing out the contacts.

```json
[
{
    "lcmId": "Unique-ID-1",
    "orgId": "YOUR_CUSTOMER_ORGID",
    "campaignId": "YOUR_CAMPAIGN_ID",
    "dialNumber": "+15557013118",
    "dialAt": "2024-01-17T00:14:28Z",
    "guardTime": "2024-01-17T23:59:00Z",
    "preferredAgentId": "",
    "customerANI": "",
    "customerData": [
    {
        "name": "LastName",
        "value": "Doe"
    },
    {
        "name": "FirstName",
        "value": "John"
    }
    ],    
    "enforceDialAtTime": true,
    "callbackContactType": "scheduled_campaign",
    "callBackPreferredAgentId": "550e8400-e29b-41d4-a716-446655440000",
    "callBackRequestTime": "2025-12-10T13:45:00.000Z",
    "callbackRequestEndTime": "2025-12-10T14:45:00.000Z",
    "scheduleId": "550e8400-e29b-41d4-a716-446655440001",
    "campaignSegment": "Campaign-Segment-1"
 }
]
```

The following table describes the fields required in the response:

| **Key**             | **Description**                                                                                                                                                                                                                     |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `lcmId`             | Vendor supplied Unique ID for the record in a vendor supplied format.                                                                                                                                                               |
| `orgId`             | The `orgId` with which the campaign is associated (UUID).                                                                                                                                                                           |
| `campaignId`        | Campaign ID with which the record is associated. It **must** match the Campaign ID provided when the campaign was started.                                                                                                          |
| `dialNumber`        | Number to dial to reach the customer. This Number should be in E164 format.                                                                                                                                                         |
| `dialAt`            | UTC time to begin dialing for the record (used in callback cases). Use the format specified in the example above.                                                                                                                   |
| `guardTime`         | UTC time to stop dialing for this record. Use the format specified in the example above.                                                                                                                                            |
| `preferredAgentId`  | TBD                                                                                                                                                                                                                                 |
| `customerANI`       | Alternate ANI to use when calling this customer. Overrides the campaign setting.                                                                                                                                                    |
| `customerData`      | Customer metadata consisting of up to **28** unique fields.                                                                                                                                                                         |
| `enforceDialAtTime` | Optional. If `enforceDialAtTime` is set to true, the dialer will attempt to dial the contact at the given `dialAt` time. If false, the `dialAt` time will not be used for dialing the call and the call can be dialed in any order. |
| `callbackContactType` | Optional. The type of callback being requested. Can take values "scheduled_campaign", "scheduled_campaign_personal", or None. "scheduled_campaign_personal" requests a personal callback, "scheduled_campaign" represents a normal scheduled callback, and None indicates it's not a callback. |
| `callBackPreferredAgentId` | Optional. If a personal callback is requested, this represents the agentId. The agentId is in UUID format (ciUserId). |
| `callBackRequestTime` | Optional. The requested start time to call back the customer, in UTC time. Format: "2025-12-10T13:45:00.000Z" |
| `callbackRequestEndTime` | Optional. The requested end time to call back the customer, in UTC time. Format: "2025-12-10T13:45:00.000Z" |
| `scheduleId` | Optional. A unique ID (UUID) to send back when the callback is invoked to correlate it to the original request. The same schedule ID will be used for each repeated retry of the callback. |
| `campaignSegment` | Optional. The individual underlying campaign which is potentially contained within the Campaign Group. |

**Note:** For IVR Campaigns, if one wants to control what time a contact should be dialed, the contact list must have a value specified for the "dialAt" field and the “enforceDialAtTime” field set true.
