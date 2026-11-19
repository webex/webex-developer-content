---
type: Guide
title: Campaign Manager Outbound Dialers
display_title: Campaign Manager Outbound Dialers
canonical_url: https://developer.webex.com/docs/campaign-manager-outbound-dialers
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/campaign-manager-outbound-dialers)

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


## Connecting to the Webex Contact Center

A custom connector is required to enable the Webex Contact Center to authenticate with your Call Manager resource domain.  This connector is utilized by the Dialer only to obtain the token for subsequent requests to the Campaign Manager. To configure the connector:

1. Login into Webex Admin Portal (Control Hub): [https://admin.webex.com](https://admin.webex.com).
2. Choose **Contact Center** in the left-hand navigation.
3. Scroll down to **Integrations** under **TENANT SETTINGS**.
4. In the **Integrations** page choose **Custom Connectors** to register your campaign manager’s URL.
5. Enter the information requested in **Set Up Custom Connector**.  The custom connector name must be **CampaignManagerCredential**

**Note:** Once your Campaign Manager endpoint is authenticated, the fetch list URI and the call disposition URI can be relative paths that use the same authentication tokens.


## Using the Webex Contact Center Campaign Manager APIs

WebexCC Campaign Manager APIs can be used to start, stop and update a campaign.  Details can be found at: [Campaign Manager](https://developer.webex.com/docs/api/v1/campaign-manager).

### Start Campaign Request:
Used to start a campaign.  For each campaign, the campaign id and dialing list fetch URL should be unique.

```bash
curl --request POST \
   --url 'https://api.wxcc-YOUR_DC.cisco.com/v1/dialer/campaign' \
   --header 'Accept: application/json' \
   --header 'Authorization: Bearer YOUR_USER_TOKEN' \
   --header 'Content-Type: application/json' \
   --data '{
     "id": "YOUR_CAMPAIGN_ID",
     "vendorVersion": "YOUR_VERSION",
     "campaignType": "YOUR_CAMPAIGN_TYPE",
     "campaignName": "",
     "authToken": "",
     "dialingRate": "1.0",
     "recordCount": "50",
     "entryPointId": "WXCC_CONFIGURED_OUTDIAL_EPID",
     "dialingListFetchURL": "YOUR_DIALINGLIST_FETCHURL",
     "outdialANI": "WXCC_CONFIGURED_OUTDIAL_ANI",
     "noAnswerRingLimit": "32",
     "maxDialingRate": "10.0",
     "abandonRatePercentage": "3.0",
     "predictiveCorrectionPace": "70",
     "predictiveGain": "1.0",
     "reservationPercentage": "100",
     "callProgressAnalysisParams": {
           "cpaEnabled": false, 
           "amdEnabled": false,
           "minSilencePeriod": "608",
           "analysisPeriod": "1000",
           "minimumValidSpeech": "112",
           "maxTimeAnalysis": "4000",
           "maxTermToneAnalysis": "30000",
           "terminatingToneDetect": false
      },
      "ivrPorts": "10",
      "previewOfferTimeout": 300,
      "previewOfferTimeoutAutoAction": "ACCEPT",
      "previewActionsDisabled": ["SKIP", "REMOVE"],
      "validCampaignTimes": {
        "timeZone": "America/New_York",
        "weeklySchedule": {
          "monday": [
            {
              "start": "09:00",
              "end": "13:00"
            },
            {
              "start": "14:00",
              "end": "18:00"
            }
          ],
          "tuesday": [
            {
              "start": "09:00",
              "end": "17:00"
            }
          ],
          "wednesday": [
            {
              "start": "10:00",
              "end": "14:00"
            }
          ],
          "thursday": [
            {
              "start": "09:00",
              "end": "13:00"
            },
            {
              "start": "14:00",
              "end": "18:00"
            }
          ],
          "friday": [
            {
              "start": "09:00",
              "end": "12:00"
            }
          ],
          "saturday": [
            {
              "start": "10:00",
              "end": "15:00"
            }
          ],
          "sunday": []
        },
        "dateOverrides": [
          {
            "date": "2025-08-15",
            "shiftTimes": [
              {
                "start": "11:00",
                "end": "16:00"
              }
            ]
          }
        ]
      }
   }'
```

| **Field Name**                 | **Description**                                                                                                                                                                                                                               |
|--------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `YOUR_DC`                      | The name of the DC where the org resides, ex: prodeu1, produs1, etc..                                                                                                                                                                         |
| `YOUR_USER_TOKEN`              | The user token associated with your org                                                                                                                                                                                                       |
| `YOUR_CAMPAIGN_ID`             | The unique id with which the Campaign Request will be started, maximum length 64 characters.                                                                                                                                                  |
| `WXCC_CONFIGURED_OUTDIAL_EPID` | Webex Contact Center outdial entry point, maximum length 36 characters.  An outdial entry point needs to be configured for each campaign.                                                                                                     |
| `YOUR_DIALINGLIST_FETCHURL`    | The unique URL the dialer will use to fetch the list of contacts to dial for the campaign, maximum length 1024 characters.  Provided by the campaign manager.  ex: https://cm.domain.com/WebService/api/v1/campaign/<campaignId>/dialinglist/ |
| `WXCC_CONFIGURED_OUTDIAL_ANI`  | Webex Contact Center outdial ANI.  This is the ANI (E164) that will be presented to the and must be restricted to the configured outdial entry points, maximum length 50 characters                                                           |



### Update Campaign Request:  
Used update a campaign, only certain parameters for a running campaign can be updated.

```bash
curl --request PUT \
  --url 'https://api.wxcc-YOUR_DC.cisco.com/v1/dialer/campaign/YOUR_CAMPAIGN_ID' \
  --header 'Accept: application/json' \
  --header 'Authorization: Bearer YOUR_USER_TOKEN' \
  --header 'Content-Type: application/json' \
  --data '{
    "dialingRate": "1.3",
    "campaignName": "",
    "authToken": "",
    "dialingListFetchURL": "YOUR_DIALINGLIST_FETCHURL",
    "outdialANI": "WXCC_CONFIGURED_OUTDIAL_ANI",
    "noAnswerRingLimit": "32",
    "maxDialingRate": "10.0",
    "reservationPercentage": "100",
    "previewOfferTimeout": 60,
    "previewOfferTimeoutAutoAction": "SKIP",
    "previewActionsDisabled": ["REMOVE"],
    "validCampaignTimes": {
      "timeZone": "America/New_York",
      "weeklySchedule": {
        "monday": [
          {
            "start": "09:00",
            "end": "13:00"
          },
          {
            "start": "14:00",
            "end": "18:00"
          }
        ],
        "tuesday": [
          {
            "start": "09:00",
            "end": "17:00"
          }
        ],
        "wednesday": [
          {
            "start": "10:00",
            "end": "14:00"
          }
        ],
        "thursday": [
          {
            "start": "09:00",
            "end": "13:00"
          },
          {
            "start": "14:00",
            "end": "18:00"
          }
        ],
        "friday": [
          {
            "start": "09:00",
            "end": "12:00"
          }
        ],
        "saturday": [
          {
            "start": "10:00",
            "end": "15:00"
          }
        ],
        "sunday": []
      },
      "dateOverrides": [
        {
          "date": "2025-08-15",
          "shiftTimes": [
            {
              "start": "11:00",
              "end": "16:00"
            }
          ]
        }
      ]
    }
  }'
```

| **Field Name**                | **Description**                                                                                                                                                                                                                               |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `YOUR_DC`                     | The name of the DC where the org resides, ex: prodeu1, produs1, etc..                                                                                                                                                                         |
| `YOUR_USER_TOKEN`             | The user token associated with your org                                                                                                                                                                                                       |
| `YOUR_CAMPAIGN_ID`            | The unique id with which the Campaign Request will be started, maximum length 64 characters.                                                                                                                                                  |
| `YOUR_DIALINGLIST_FETCHURL`   | The unique URL the dialer will use to fetch the list of contacts to dial for the campaign, maximum length 1024 characters.  Provided by the campaign manager.  ex: https://cm.domain.com/WebService/api/v1/campaign/<campaignId>/dialinglist/ |
| `WXCC_CONFIGURED_OUTDIAL_ANI` | Webex Contact Center outdial ANI.  This is the ANI (E164) that will be presented to the and must be restricted to the configured outdial entry points, maximum length 50 characters                                                           |



### Stop Campaign Request:  
Used to stop a campaign.

```bash
curl --request DELETE \
  --url 'https://api.wxcc-YOUR_DC.cisco.com/v1/dialer/campaign/YOUR_CAMPAIGN_ID' \
  --header 'Authorization: Bearer YOUR_USER_TOKEN'
```

| **Field Name**     | **Description**                                                                              |
|--------------------|----------------------------------------------------------------------------------------------|
| `YOUR_DC`          | The name of the DC where the org resides, ex: prodeu1, produs1, etc..                        |
| `YOUR_USER_TOKEN`  | The user token associated with your org                                                      |
| `YOUR_CAMPAIGN_ID` | The unique id with which the Campaign Request will be started, maximum length 64 characters. |


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
