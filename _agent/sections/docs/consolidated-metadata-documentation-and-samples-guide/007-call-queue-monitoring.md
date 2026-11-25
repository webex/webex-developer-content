---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Queue - Scenarios
- Call Queue - Monitoring
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Parent context

## Call Queue - Scenarios

1. PSTN Caller: 1001, .
2. Webex Calling Agent: 5050,  (`sip:dtl98hsajj`) (Recording Enabled).
3. Webex Calling Supervisor: 5060 (`sip:x4y6xdsegz`) (Recording Enabled).
4. Call Queue: .
5. PSTN Caller calls the Webex Calling Agent. The Supervisor will perform an action (takeover, barge in, or monitor).

## Selected section

### Call Queue - Monitoring

#### Metadata - Agent

```json
{
  "id": "74455e06-65ec-4bb5-889b-8534289dd058",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "74455e06-65ec-4bb5-889b-8534289dd058",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "a6c581e9-9c4d-4868-9bdf-290041494896",
    "personality": "terminator",
    "callingParty": { //PSTN user
      "actor": null,
      "number": "",
      "name": ""
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
      },
      "number": "",
      "name": "user1(å‘¨æž—)"
    },
    "callId": "callhalf-2179003:0",
    "session": {
      "startTime": "2024-04-17T09:12:27Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-17T09:12:27Z",
        "mediaStreams": [
          {
            "streamId": "3df80b53-cfaf-49c4-99b2-18733fb52ef1",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "sip:@X.X.X.X",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
            },
            "number": "sip:@X.X.X.X",
            "name": null
          },
          "numOfRedirections": 1
        },
        "redirectedCall": null,
        "acd": {
          "actor": {
            "type": "USER",
            "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
          },
          "acdName": "CallQueuePSTNTest",
          "acdNumber": {
            "user": null,
            "countryCode": "1",
            "number": null
          }
        },
        "announcementData": null
      },
      {
        "timeStamp": "2024-04-17T09:13:27Z",
        "mediaStreams": null, // This is a known limitation/bug.
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": null, // Supervisor Info aren't captured anywhere to know whether supervisor is Monitoring.
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "3df80b53-cfaf-49c4-99b2-18733fb52ef1"
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "sip:@X.X.X.X",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
            },
            "number": "sip:@X.X.X.X",
            "name": null
          },
          "numOfRedirections": 1
        },
        "redirectedCall": { //From, To party are same
          "newExtTrackingId": "f2a2e4ab-b7f5-4a92-b51a-e119b7c0d8b1",
          "redirectedFromPartyNumber": "",
          "redirectedToPartyNumber": "sip:@X.X.X.X;user=phone"
        },
        "acd": {
          "actor": {
            "type": "USER",
            "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
          },
          "acdName": "CallQueuePSTNTest",
          "acdNumber": {
            "user": null,
            "countryCode": "1",
            "number": null
          }
        },
        "announcementData": null
      },
      {
        "timeStamp": "2024-04-17T09:14:23Z",
        "mediaStreams": [
          {
            "streamId": "9819fbae-1025-4089-b793-46de30f13727",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "9819fbae-1025-4089-b793-46de30f13727"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "9819fbae-1025-4089-b793-46de30f13727"
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "sip:@X.X.X.X",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
            },
            "number": "sip:@X.X.X.X",
            "name": null
          },
          "numOfRedirections": 1
        },
        "redirectedCall": {
          "newExtTrackingId": "d6bc7ef9-72fd-4e58-945a-a5a74c584144",
          "redirectedFromPartyNumber": "",
          "redirectedToPartyNumber": "sip:@X.X.X.X;user=phone"
        },
        "acd": {
          "actor": {
            "type": "USER",
            "id": "7257fde6-12b4-4b2a-a51b-d07c035c02aa"
          },
          "acdName": "CallQueuePSTNTest",
          "acdNumber": {
            "user": null,
            "countryCode": "1",
            "number": null
          }
        },
        "announcementData": null
      }
    ]
  }
}
```

#### Metadata - Supervisor with Agent

```json
{
  "id": "cf1b0d9e-4e0b-4d31-a105-491e09ce2c8d",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "cf1b0d9e-4e0b-4d31-a105-491e09ce2c8d",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "f2a2e4ab-b7f5-4a92-b51a-e119b7c0d8b1",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
      },
      "number": "5060",
      "name": "bob"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
      },
      "number": "5050",
      "name": "user1(å‘¨æž—)"
    },
    "callId": "callhalf-2186717:0",
    "session": {
      "startTime": "2024-04-17T09:13:28Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-17T09:13:28Z",
        "mediaStreams": [
          {
            "streamId": "3583b25a-58ff-40cb-be4b-9c816e9f69c4",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
            },
            "aor": "sip:x4y6xdsegz@******",
            "send": "3583b25a-58ff-40cb-be4b-9c816e9f69c4"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:5050@X.X.X.X;user=phone",
            "send": "3583b25a-58ff-40cb-be4b-9c816e9f69c4"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X",
            "send": "3583b25a-58ff-40cb-be4b-9c816e9f69c4"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-17T09:13:29Z",
          "announcementParticipants": [
            "sip:x4y6xdsegz@******"
          ],
          "announcementType": "USER_LEVEL"
        }
      }
    ]
  }
}
```

#### Metadata - Supervisor with PSTN User

```json
{
  "id": "3701f22a-fb1d-4e17-9af8-80e73c60a2a5",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "3701f22a-fb1d-4e17-9af8-80e73c60a2a5",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "38e1a9eb-00b7-44a9-89f0-4d0128a03e5a",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "",
      "name": ""
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
      },
      "number": "5060",
      "name": "bob"
    },
    "callId": "callhalf-2186717:1",
    "session": {
      "startTime": "2024-04-17T09:13:28Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-17T09:13:28Z",
        "mediaStreams": [
          {
            "streamId": "cbdf3756-ba0b-4e8a-99b4-683ba820b7b3",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
            },
            "aor": "sip:x4y6xdsegz@******",
            "send": "cbdf3756-ba0b-4e8a-99b4-683ba820b7b3"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "cbdf3756-ba0b-4e8a-99b4-683ba820b7b3"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "cbdf3756-ba0b-4e8a-99b4-683ba820b7b3"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": null
      }
    ]
  }
}
```
