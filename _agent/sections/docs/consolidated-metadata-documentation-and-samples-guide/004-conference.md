---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Conference
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

## Conference

Scenarios

1. 8009 calls 8008.
2. 8008 conferences 8007.

All three are in calls with recording enabled.

#### Conference

```json
{
  "id": "bd5dd6a2-4f46-413c-aa3e-c1592309f678",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "134fe7d8-800c-474a-9b15-9458d9103ad1",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "bd5dd6a2-4f46-413c-aa3e-c1592309f678",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "1be0d748-f352-4482-9df1-313322269e19",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
      },
      "number": "8008",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
      },
      "number": "8007",
      "name": "bob"
    },
    "callId": "callhalf-:1",
    "session": {
      "startTime": "2024-04-12T04:13:08Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-12T04:13:08Z",
        "mediaStreams": [
          {
            "streamId": "dba9765e-c3cf-409d-9d68-29248db56ebc",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
          },
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:8007@X.X.X.X;user=phone",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "teshwamb9u@******",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-12T04:13:09Z",
          "announcementParticipants": [
            "sip:nyi9lt4urv@******",
            "sip:8007@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      }
    ]
  }
}
```

#### Important Fields



> **Info**
>
> There is an inconsistency in presenting the user number. In some sections, it's presented as a Number, and in other places, it's presented as a SIP AoR. This will be fixed in subsequent releases.



See the following example:

1. "sip:nyi9lt4urv@******" refers to the user with the number 8008.
2. "teshwamb9u@******" refers to the user with the number 8009.

#### Participants

```json
{
    "participants": [
        {
            "actor": {
                "type": "USER",
                "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
        },
        {
            "actor": {
                "type": "USER",
                "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:8007@X.X.X.X;user=phone",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
        },
        {
            "actor": {
                "type": "USER",
                "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "teshwamb9u@******",
            "send": "dba9765e-c3cf-409d-9d68-29248db56ebc"
        }
    ]
}
```
