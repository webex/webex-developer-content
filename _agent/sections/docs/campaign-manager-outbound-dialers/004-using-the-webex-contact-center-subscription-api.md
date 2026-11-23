---
type: Excerpt
canonical_url: https://developer.webex.com/docs/campaign-manager-outbound-dialers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Webex Contact Center Subscription API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/campaign-manager-outbound-dialers). [Full Markdown](../../../../docs/campaign-manager-outbound-dialers.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Campaign Manager Requirements](001-campaign-manager-requirements.md)

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

## Using the Webex Contact Center Subscription API

For the Campaign Manager to handle the outcome of the provided customer records, a subscription needs to be registered in order to listen for dialer related events.

Based on the processing of a contact, the Dialer service will publish the outcome via an event.  These events are forwarded to users subscribed to the **campaign:contact-disposition** event.  Campaign Managers can then use these events to decide how contacts of the campaign are handled by rescheduling, closing or doing a retry immediately.  Or, contact outcomes can be grouped and sorted for analysis.

**Note:** The webhook receiver **must** be performant and be able to sufficiently handle the call rate. If the receiver does not respond within 5 seconds, the webhook will be considered a failed post.

Details on the Register Subscription API can be found at: [Register Subscription](https://developer.webex.com/docs/api/v1/subscriptions/register-subscription).

Here’s a sample curl command that registers to receive call dispositions:

```bash
curl --request POST \
  --url 'https://api.wxcc-YOUR_DC.cisco.com/v2/subscriptions \
  --header 'Accept: application/json' \
  --header 'Authorization: Bearer YOUR_USER_TOKEN' \
  --header 'Content-Type: application/json' \
   --data '{
    "name": "YOUR_CAMPAIGN_MANAGER_SUBSCRIPTION",
    "description": "Connects campaign manager to WXCC Outbound Dialer",
    "eventTypes": [
      "campaign:contact-disposition"
    ],
    "destinationUrl": "YOUR_CAMPAIGN_MANAGER_URL”,
    "secret": "YOUR_SECRET",
    "orgId": "YOUR_CUSTOMER_ORGID",
    "resourceVersion": "campaign:1.0.0"    
  }'
```

Multiple records can be included in a single message. If the command is successful, you’ll see a response similar to the following example which shows how a contact-disposition event with 2 records is formatted.

```json
{
"data": [{
    "contactId": "Unique-ID-1",
    "destination": "5551112345",
    "taskId": "199dda6a-3018-4b1c-bd4f-55519343b253",
    "telephonyOutcome": 3,
    "businessOutcome": null,
    "agentId": "",
    "callbackPreferredAgentId": "",
    "callStartTime": "2023-12-01T16:11:34.794Z",
    "callEndTime": null,
    "callbackContactType": "scheduled_campaign",
    "callbackEndTime": "2025-12-10T13:45:00.000Z",
    "scheduleId": "550e8400-e29b-41d4-a716-446655440000"
},{
    "contactId": "Unique-ID-2",
    "destination": 5551116789,
    "taskId": "1fafff97-e821-4a35-b94b-20ef22388b4e",
    "telephonyOutcome": 3,
    "businessOutcome": null,
    "agentId": "",
    "callbackPreferredAgentId": "",
    "callStartTime": "2023-12-01T16:11:34.812Z",
    "callEndTime": null,
    "callbackContactType": "scheduled_campaign_personal",
    "callbackEndTime": "2025-12-10T14:45:00.000Z",
    "scheduleId": "550e8400-e29b-41d4-a716-446655440001"
}],
    "id": "757f4bf9-9672-4a07-a964-38b3d0eb7664",
    "source": "/com/cisco/wxcc/d6159130-7d37-4dc1-aba8-7ef56fb099d7",
    "specversion": "1.0",
    "type": "campaign:contact-disposition",
    "datacontenttype": "application/json",
    "comciscoorgid": "YOUR_CUSTOMER_ORGID",
    "campaignId": "YOUR_CAMPAIGN_ID"
}
```

The following table describes the keys returned in the response:

| **Key**                           | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `contactId`                       | The unique ID supplied when the record was retrieved.                                                                                                                                                                                                                                                                                                                                                                          |
| `destination`                     | Customer dialed number provided when the record was retrieved.                                                                                                                                                                                                                                                                                                                                                                 |
| `taskId`                          | The `interactionId` of the customer call                                                                                                                                                                                                                                                                                                                                                                                       |
| `campaignId`                      | Campaign ID with which the record is associated with. Must match the Campaign ID when the campaign was started.                                                                                                                                                                                                                                                                                                                |
| `telephonyOutcome`                | State of the contact at the end of the call. See the Description Of Telephone Outcomes table below for the complete code-name and ID mapping. |
| `businessOutcome` (if Applicable) | The WXCC auxiliary codes that the agent can enter as an outcome of the call.                                                                                                                                                                                                                                                                                                                                                   |
| `callbackPreferredAgentId`        | N/A                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `agentId`                         | ID of the agent who answered the call (UUID).                                                                                                                                                                                                                                                                                                                                                                                  |
| `callbackTime`                    | N/A                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `callStartTime`                   | UTC call start time.d                                                                                                                                                                                                                                                                                                                                                                                                          |
| `callEndTime`                     | UTC call end time.                                                                                                                                                                                                                                                                                                                                                                                                             |
| `callbackContactType`             | The type of callback being requested. Can take values "scheduled_campaign", "scheduled_campaign_personal", or None. "scheduled_campaign_personal" requests a personal callback, "scheduled_campaign" represents a normal scheduled callback, and None indicates it's not a callback.                                                                                                                                                                                                   |
| `callbackEndTime`                 | The end time to call back the customer, in UTC time. Format: "2025-12-10T13:45:00.000Z"                                                                                                                                                                                                                                                                                                                                        |
| `scheduleId`                      | A unique ID (UUID) to send back when the callback is invoked to correlate it to the original request. The same schedule ID will be used for each repeated retry of the callback.                                                                                                                                                                                                                                              |


### Description Of Telephone Outcomes ###

The following table describes the various `telephonyOutcome` values:

| **Code Name**          | **Description**                                                         | **ID** |
|------------------------|-------------------------------------------------------------------------|--------|
| `INVALID_NUMBER`       | Number not in service.                                                  | 1      |
| `NO_ANSWER`            | Customer did not answer.                                                | 2      |
| `BUSY`                 | Number was busy.                                                        | 3      |
| `FAX`                  | FAX machine detected.                                                   | 4      |
| `AMD`                  | Answering machine detected.                                             | 5      |
| `NETWORK_VOICEMAIL`    | Network answering machine / voicemail.                                  | 6      |
| `NO_RINGBACK`          | Error condition on network (temporary).                                 | 7      |
| `OPERATOR_INTERCEPT`   | Error condition on network (temporary).                                 | 8      |
| `CALLBACK_REQUESTED`   | Customer requested callback.                                            | 9      |
| `ABANDONED`            | Abandoned by the dialer.                                                | 10     |
| `ABANDONED_TO_IVR`     | Abandoned by the dialer and redirected to IVR.                          | 11     |
| `FLUSHED_CAMP_STOP`    | Record flushed due to campaign end / stop.                              | 12     |
| `GUARD_TIME_EXPIRY`    | The guard time for the record expired.                                  | 13     |
| `FLUSHED_ERROR`        | Flushed due to a system error OR Agent canceled a preview call.         | 14     |
| `DNC_REQUESTED`        | Customer asked to be placed on the DNC list.                            | 15     |
| `LIVE_VOICE`           | Live voice detected.                                                    | 16     |
| `INVALID_CAD`          | CAD Map Size Exceeds Limit.                                             | 17     |
| `DIAL_AT_TIME_INVALID` | The `dialAt` time is not valid (too late to dial as per configuration). | 18     |
| `PREVIEW_SKIPPED`      | Record skipped when in preview.                                         | 19     |
| `PREVIEW_REMOVED`      | Record removed when in preview.                                         | 20     |
| `CUSTOMER_ABANDONED`   | Customer Abandoned the call.                                            | 21     |
| `AGENT_UNAVAILABLE`    | The dialer could not obtain the requested agent for a personal scheduled callback, or any agent for a non-personal scheduled callback, during the callback window. | 22     |
