---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Transfer
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

## Transfer

User Details:

1. PSTN Caller: .
2. Webex Calling User 1: E164 number  with Extension 5050 and SIP AoR `sip:dtl98hsajj` (Recording Enabled).
3. Webex Calling User 2: E164 number  with extension 5060 (Recording Enabled).

### Blind Transfer

#### Metadata - Webex Calling User 1

```json
{
  "id": "336bd3ca-d9a2-49a1-847d-a32c52e7d63a",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "336bd3ca-d9a2-49a1-847d-a32c52e7d63a",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "3d140d07-b97b-4ac0-9376-43c993a1a53e",
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
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-16T09:59:45Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-16T09:59:45Z",
        "mediaStreams": [
          {
            "streamId": "80eab853-ab77-47e9-8623-da18ae87b5f6",
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
            "send": "80eab853-ab77-47e9-8623-da18ae87b5f6"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "80eab853-ab77-47e9-8623-da18ae87b5f6"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/ComplianceAnnouncement.wav",
          "announcementTimestamp": "2024-04-16T09:59:41Z",
          "announcementParticipants": [
            "sip:@X.X.X.X"
          ],
          "announcementType": "COMPLIANCE"
        }
      }
    ]
  }
}
```

#### Metadata - Webex Calling User 2

```json
{
  "id": "8aabd8c2-c7fa-47f0-bfb0-12dd06a89019",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "8aabd8c2-c7fa-47f0-bfb0-12dd06a89019",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "3d140d07-b97b-4ac0-9376-43c993a1a53e",
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
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-16T10:00:09Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-16T10:00:09Z",
        "mediaStreams": [
          {
            "streamId": "75bc11f5-5bf2-408c-bbc4-c70c1305f956",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {   //Webex user
              "type": "USER",
              "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
            },
            "aor": "sip:x4y6xdsegz@******",
            "send": "75bc11f5-5bf2-408c-bbc4-c70c1305f956"
          },
          {
            "actor": null, //PSTN user
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "75bc11f5-5bf2-408c-bbc4-c70c1305f956"
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "sip:5060@X.X.X.X",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1" //Webex Calling User(5050, )
            },
            "number": "sip:@X.X.X.X",
            "name": null 
          },
          "numOfRedirections": 1
        },
        "redirectedCall": null,
        "acd": null,
        "announcementData": null
      }
    ]
  }
}
```

### Consult Transfer

#### Metadata - Webex Calling User 1 before Transfer

```json
{
  "id": "406c762d-a4a7-4215-870a-9f8cf7814282",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "406c762d-a4a7-4215-870a-9f8cf7814282",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "05f36128-fc65-47c8-8b88-4e77706b7db6",
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
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-16T10:16:05Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-16T10:16:05Z",
        "mediaStreams": [
          {
            "streamId": "e96ca188-6bdd-47d7-ba1e-74e167bb277d",
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
            "send": "e96ca188-6bdd-47d7-ba1e-74e167bb277d"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "e96ca188-6bdd-47d7-ba1e-74e167bb277d"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/ComplianceAnnouncement.wav",
          "announcementTimestamp": "2024-04-16T10:15:58Z",
          "announcementParticipants": [
            "sip:@X.X.X.X"
          ],
          "announcementType": "COMPLIANCE"
        }
      }
    ]
  }
}
```

#### Metadata - Webex Calling User 1 during Transfer

```json
{
  "id": "2eb36bcf-2d36-4ef7-a924-ccd5638140c7",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1",
  "ownerType": "USER",
  "ownerName": "alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "2eb36bcf-2d36-4ef7-a924-ccd5638140c7",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "59b33fe3-ebec-44d8-82f5-a5e7cc814aa6",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
      },
      "number": "",
      "name": "user1(å‘¨æž—)"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
      },
      "number": "5060",
      "name": "bob"
    },
    "callId": "callhalf-:1",
    "session": {
      "startTime": "2024-04-16T10:16:41Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-16T10:16:41Z",
        "mediaStreams": [
          {
            "streamId": "3bc33992-4f55-4aeb-82d0-8b411095cd7e",
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
            "send": "3bc33992-4f55-4aeb-82d0-8b411095cd7e"
          },
          {
            "actor": {
              "type": "USER",
              "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
            },
            "aor": "sip:5060@X.X.X.X;user=phone",
            "send": "3bc33992-4f55-4aeb-82d0-8b411095cd7e"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-16T10:16:42Z",
          "announcementParticipants": [
            "sip:dtl98hsajj@******",
            "sip:5060@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      }
    ]
  }
}
```

#### Metadata - Webex Calling User 2

```json
{
  "id": "86dfe561-3c35-4dc4-8f2b-54dd79c3b391",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4",
  "ownerType": "USER",
  "ownerName": "bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "86dfe561-3c35-4dc4-8f2b-54dd79c3b391",
    "locationId": "7ad65b32-2bb2-40ec-bd19-d1eb7265481d",
    "callSessionId": "59b33fe3-ebec-44d8-82f5-a5e7cc814aa6",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
      },
      "number": "5050",
      "name": "user1(å‘¨æž—)"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "90f74442-41bb-42e4-9bdb-ff7b43ed0ca4"
      },
      "number": "5060",
      "name": "bob"
    },
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-16T10:16:40Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-16T10:16:40Z",
        "mediaStreams": [
          {
            "streamId": "b719797d-f90b-4467-b90c-c078eff89a6b",
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
            "send": "b719797d-f90b-4467-b90c-c078eff89a6b"
          },
          {
            "actor": {
              "type": "USER",
              "id": "7c216e91-c5d1-47b5-9b6d-ccfd05481ed1"
            },
            "aor": "sip:5050@X.X.X.X;user=phone",
            "send": "b719797d-f90b-4467-b90c-c078eff89a6b"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-16T10:16:41Z",
          "announcementParticipants": [
            "sip:x4y6xdsegz@******",
            "sip:5050@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      },
      {
        "timeStamp": "2024-04-16T10:16:58Z",
        "mediaStreams": [
          {
            "streamId": "df3cb58c-c78d-48c7-b5ce-b9518ed79469",
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
            "send": "df3cb58c-c78d-48c7-b5ce-b9518ed79469"
          },
          {
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "df3cb58c-c78d-48c7-b5ce-b9518ed79469"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": {
          "newExtTrackingId": "221aca5d-0803-4ff1-9bac-49a6fd82450d",
          "redirectedFromPartyNumber": "5050",
          "redirectedToPartyNumber": "sip:@X.X.X.X;user=phone"
        },
        "acd": null,
        "announcementData": null
      }
    ]
  }
}
```
