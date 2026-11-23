---
type: Excerpt
canonical_url: https://developer.webex.com/docs/campaign-manager-outbound-dialers
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Using the Webex Contact Center Campaign Manager APIs
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
