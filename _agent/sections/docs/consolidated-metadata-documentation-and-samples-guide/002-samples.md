---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Samples
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

## Samples

Samples of metadata output is shown here explaining the metadata for basic call and various webex calling scenarios such as consult transfer, blind transfer, conference and call queue features.

### Basic Call with Announcement

Scenario

1. 8007 calls 8008. Recording enabled for both users with announcement.

#### Metadata - 8008

```json
{
  "id": "42a22e15-7bd0-49f9-a6b6-d6d86a13ebfa",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "134fe7d8-800c-474a-9b15-9458d9103ad1",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "42a22e15-7bd0-49f9-a6b6-d6d86a13ebfa",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "a0b6e7b7-cde6-415e-94b2-e02b58feb749",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
      },
      "number": "8007",
      "name": ". bob"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
      },
      "number": "8008",
      "name": ". alice"
    },
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-02T08:33:39Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-04-02T08:33:39Z",
        "mediaStreams": [
          {
            "streamId": "ff5c6eca-3ffe-4f63-bbb4-0b6821077368",
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
            "send": "ff5c6eca-3ffe-4f63-bbb4-0b6821077368"
          },
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:8007@X.X.X.X;user=phone",
            "send": "ff5c6eca-3ffe-4f63-bbb4-0b6821077368"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-02T08:33:41Z",
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

### Pause/Resume

Scenarios

1. 8007 calls 8008. Recording enabled for both users with start announcement.
2. Pause/Resume announcement disabled.

#### Metadata - 8007 (Pause/Resume Announcement Disabled)

```json
{
  "id": "fb2d0ad8-2f1d-483b-bd16-733dfbb5c97b",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0",
  "ownerType": "USER",
  "ownerName": ". bob",
  "ownerEmail": "bob@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "fb2d0ad8-2f1d-483b-bd16-733dfbb5c97b",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "711496f6-4f40-403c-8138-09fe9e8070a1",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
      },
      "number": "",
      "name": ". bob"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
      },
      "number": "8008",
      "name": ". alice"
    },
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-02T11:10:57Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [
      {
        "action": "PAUSE",
        "time": "2024-04-02T11:11:22Z"
      },
      {
        "action": "RESUME",
        "time": "2024-04-02T11:11:45Z"
      }
    ],
    "callActivity": [
      {
        "timeStamp": "2024-04-02T11:10:57Z",
        "mediaStreams": [
          {
            "streamId": "92b6692b-bb20-431d-b887-d2bf20c6f5c2",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": "92b6692b-bb20-431d-b887-d2bf20c6f5c2"
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": "92b6692b-bb20-431d-b887-d2bf20c6f5c2"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-02T11:11:00Z",
          "announcementParticipants": [
            "sip:qilz560c9a@******",
            "sip:8008@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      },
      {
        "timeStamp": "2024-04-02T11:11:22Z",
        "mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-02T11:11:00Z",
          "announcementParticipants": [
            "sip:qilz560c9a@******",
            "sip:8008@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      },
      {
        "timeStamp": "2024-04-02T11:11:45Z",
        "mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-02T11:11:00Z",
          "announcementParticipants": [
            "sip:qilz560c9a@******",
            "sip:8008@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      }
    ]
  }
```

### Important Fields

There are 3 different call activity object at 3 timestamps:

1. Time the recording started.
2. Time the recording was paused.
3. Time time the recording was resumed.

If the announcement for pause/resume is enabled, it is reflected in the second and third call activity objects.

#### Recording Action

```json
"recordingActions": [
      {
        "action": "PAUSE",
        "time": "2024-04-02T11:11:22Z"
      },
      {
        "action": "RESUME",
        "time": "2024-04-02T11:11:45Z"
      }
    ]
```

The "Pause Call Activity" block shows participants with a `null` `send` attribute.

#### Pause - Participants

```json
"mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "2ebbe39b-d41d-47ac-9347-cd07ce233bc0"
            },
            "aor": "sip:qilz560c9a@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:8008@X.X.X.X;user=phone",
            "send": null
          }
        ]
```

Scenario 2:

1. 8009 calls 8008.
2. Pause/Resume is enabled with announcement.

#### Metadata - 8008 (Pause/Resume Announcement Enabled)

```json
{
  "id": "8d9af94b-5f0c-46c3-8e96-02a9cbfe3763",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "134fe7d8-800c-474a-9b15-9458d9103ad1",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "JP",
  "serviceType": "calling",
  "version": "1.0",
  "serviceData": {
    "callRecordingId": "8d9af94b-5f0c-46c3-8e96-02a9cbfe3763",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "7bf4354e-be45-4e0c-bb73-7591f71d0034",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
      },
      "number": "8009",
      "name": "carol"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
      },
      "number": "8008",
      "name": "alice"
    },
    "callId": "callhalf-:0",
    "session": {
      "startTime": "2024-04-12T06:42:56Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [
      {
        "action": "RESUME",
        "time": "2024-04-12T06:43:29Z"
      },
      {
        "action": "PAUSE",
        "time": "2024-04-12T06:43:08Z"
      }
    ],
    "callActivity": [
      {
        "timeStamp": "2024-04-12T06:42:56Z",
        "mediaStreams": [
          {
            "streamId": "d9638230-0025-4f5e-a2fb-0e12e86b97f7",
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
            "send": "d9638230-0025-4f5e-a2fb-0e12e86b97f7"
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "sip:8009@X.X.X.X;user=phone",
            "send": "d9638230-0025-4f5e-a2fb-0e12e86b97f7"
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingResumed.wav",
          "announcementTimestamp": "2024-04-12T06:43:29Z",
          "announcementParticipants": [
            "sip:nyi9lt4urv@******",
            "sip:8009@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      },
      {
        "timeStamp": "2024-04-12T06:43:08Z",
        "mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "sip:8009@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "sip:8009@X.X.X.X;user=phone",
            "send": null
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingStarted.wav",
          "announcementTimestamp": "2024-04-12T06:42:58Z",
          "announcementParticipants": [
            "sip:nyi9lt4urv@******",
            "sip:8009@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      },
      {
        "timeStamp": "2024-04-12T06:43:29Z",
        "mediaStreams": null,
        "participants": [
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "134fe7d8-800c-474a-9b15-9458d9103ad1"
            },
            "aor": "sip:nyi9lt4urv@******",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "sip:8009@X.X.X.X;user=phone",
            "send": null
          },
          {
            "actor": {
              "type": "USER",
              "id": "e5800f52-a361-4fb3-a85a-a298bdb52364"
            },
            "aor": "sip:8009@X.X.X.X;user=phone",
            "send": null
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": {
          "announcementFilename": "http://******/media/en_US/TrtCallRecordingPaused.wav",
          "announcementTimestamp": "2024-04-12T06:43:08Z",
          "announcementParticipants": [
            "sip:nyi9lt4urv@******",
            "sip:8009@X.X.X.X;user=phone"
          ],
          "announcementType": "USER_LEVEL"
        }
      }
    ]
  }
}
```

The announcement file names "http://*****.com/media/en_US/TrtCallRecordingPaused.wav" and "http://*****.com/media/en_US/TrtCallRecordingResumed.wav" can be seen in the call activity blocks.
