---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Queue - Scenarios
- Call Queue - Take Over
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

### Call Queue - Take Over

#### Metadata - Agent

```json
{
  "id": "6e175cfc-a66d-4e26-be08-376158b270e5",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "6e175cfc-a66d-4e26-be08-376158b270e5",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "252fe723-9a6d-4c00-b9ff-7b5fcf1b4148",
    "personality": "terminator",
    "callingParty": {
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
    "callId": "callhalf-2063325:0",
    "session": {
      "startTime": "2024-04-17T08:58:22Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-17T08:58:22Z",
        "mediaStreams": [
          {
            "streamId": "027792d3-f58e-4799-b9f2-72f52266001c",
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
            "send": "027792d3-f58e-4799-b9f2-72f52266001c"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "027792d3-f58e-4799-b9f2-72f52266001c"
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
      }
    ]
  }
}
```

#### Metadata - Supervisor

```json
{
  "id": "d7d7856a-fb23-4d65-a937-a73a8fae1cd9",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "d7d7856a-fb23-4d65-a937-a73a8fae1cd9",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "49cdfdb2-1fb9-44d8-a26b-b843972443c0",
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
    "callId": "callhalf-2073895:0",
    "session": {
      "startTime": "2024-04-17T08:59:42Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-17T08:59:42Z",
        "mediaStreams": [
          {
            "streamId": "96c066b0-2856-448c-9aa8-1a7eae5fda94",
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
            "send": "96c066b0-2856-448c-9aa8-1a7eae5fda94"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "96c066b0-2856-448c-9aa8-1a7eae5fda94"
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
