---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Call Queue - Scenarios
- Call Queue - Barge In
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

### Call Queue - Barge In

#### Metadata - Agent

```json
{
  "id": "8471f06d-af3f-4b80-844c-a7ae164cea5a",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "8471f06d-af3f-4b80-844c-a7ae164cea5a",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "5820b0ff-4bae-42cc-ace8-269a4b76f811",
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
    "callId": "callhalf-81316811:0",
    "session": {
      "startTime": "2024-04-24T10:14:17Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-24T10:14:17Z",
        "mediaStreams": [
          {
            "streamId": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec",
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
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
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
        "timeStamp": "2024-04-24T10:14:44Z",
        "mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:dtl98hsajj@******",
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
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
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "03388e08-a7ab-4797-9dd7-bc786cd5e3ec"
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
          "newExtTrackingId": "238803cf-2f1a-4ee6-92d8-cbe9af65df45",
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
        "timeStamp": "2024-04-24T10:15:35Z",
        "mediaStreams": [
          {
            "streamId": "9f3beb01-5d37-4341-a012-d65a2a796e9a",
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
            "send": "9f3beb01-5d37-4341-a012-d65a2a796e9a"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "9f3beb01-5d37-4341-a012-d65a2a796e9a"
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
          "newExtTrackingId": "e7ecbaa7-f11c-4b28-add5-3da4f7402543",
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
  "id": "e0d45b9e-977e-4630-8768-8d0fa1f0dc4f",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "e0d45b9e-977e-4630-8768-8d0fa1f0dc4f",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "238803cf-2f1a-4ee6-92d8-cbe9af65df45",
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
    "callId": "callhalf-81321951:0",
    "session": {
      "startTime": "2024-04-24T10:14:45Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-24T10:14:45Z",
        "mediaStreams": [
          {
            "streamId": "9511dd3a-44b2-4cb6-a1f6-f7626f089798",
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
            "send": "9511dd3a-44b2-4cb6-a1f6-f7626f089798"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:5050@X.X.X.X;user=phone",
            "send": "9511dd3a-44b2-4cb6-a1f6-f7626f089798"
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

#### Metadata - Supervisor with PSTN User

```json
{
  "id": "81f79ede-ddcf-412e-84cc-6662df8eda68",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "81f79ede-ddcf-412e-84cc-6662df8eda68",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "e71f6e2a-7b63-44b9-a37c-1d00dfc95e53",
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
    "callId": "callhalf-81321951:1",
    "session": {
      "startTime": "2024-04-24T10:14:45Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-24T10:14:45Z",
        "mediaStreams": [
          {
            "streamId": "2124ea67-8ded-4e58-9a34-d65db2ebe39a",
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
            "send": "2124ea67-8ded-4e58-9a34-d65db2ebe39a"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "2124ea67-8ded-4e58-9a34-d65db2ebe39a"
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
