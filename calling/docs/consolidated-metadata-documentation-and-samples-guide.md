---
type: Guide
title: Consolidated Metadata Documentation and Samples Guide | Consolidated Guide
display_title: Metadata and Samples
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide)

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Metadata Basic Fields

This table contains common metadata fields associated with every call recording:



| **Field**         | **Description**                                                                                       |
| ----------------- | ----------------------------------------------------------------------------------------------------- |
| `id`              | A unique identifier for the recording.                                                                |
| `orgId`           | Organization ID of the recording owner.                                                               |
| `ownerId`         | Unique identifier of the recording owner.                                                             |
| `ownerType`       | User (`USER`), Virtual Line (`VIRTUAL_LINE`), or Work Place (`PLACE`).                                |
| `ownerName`       | The full name of the recording owner.
| `ownerEmail`      | The email address of the recording owner.                                                             |
| `storageRegion`   | ISO 3166-1 alpha-2 codes that represent the 2-digit country code of the Webex storage region.         |
| `serviceType`     | Calling.                                                                                              |
| `version`         | Metadata version.                                                                                     |
| `serviceData`     | [Service Data](#service-data).                                                                        |

### Service Data

This table contains various fields that are present in serviceData section of metadata API response. This section of data is a consolidated information representing various events within a call recording:



| **Field**                 | **Description**                                                                                       |
| ------------------------- | ----------------------------------------------------------------------------------------------------- |
| `callRecordingId`         | A unique identifier for call recording in Webex Calling.                                              |
| `locationId`              | A unique identifier for the Webex Calling location.                                                   |
| `callSessionId`           | A unique identifier for the call session to which the call belongs. This can be used to correlate multiple calls that are part of the same call session. |
| `personality`             | The personality of the call (originator/terminator).                                                  |
| `callId`                  | The call identifier of the call.                                                                      |
| `recordingType`           | Identifies the type of recording enabled for the owner of the recording: "alwaysON" (Always, Always with Pause/Resume in CH), "onDemand" (On demand in CH), "voicemail" (if voicemail is enabled). |
| `callingParty/calledParty`| Details of the calling and called party. It has various fields like `actor`, `name`, and `number`. The `actor` section is applicable for Webex Users only. |
| `connectedParty`          | For outbound calls, the connected party is determined based on the identity of the remote connected party. For inbound calls, this refers to the identity of the other party (the caller) that is connected. This field is applicable for Virtual Line, Call Queue, Group Call Pickup, and similar scenarios. |
| `managedBy`               | For Virtual Line, Shared Line, Call Queue, Group Call Pickup, and similar scenarios, this indicates the device owner who handled the call. |
| `session startTime`       | Recording Start Time in UTC.                                                                          |
| `session stopTime`        | Recording Stop Time in UTC. NOTE: In this release, this field is not populated.                       |
| `answererInfo`            | [Answerer Info](#answerer-info). Optional element populated for cases like Shared lines and contains device owner information of the user who answered the call. |
| `recordingActions`        | [Recording Action](#recording-actions). Optional element added when recording pause/resume is done within a recording session. |
| `callActivity (list)`     | [Call Activity](#call-activity). Optional element that gives additional information about activities that happened during the call (e.g., transfer, redirected party information, announcement details, etc.). |

### Calling and Called Party

This table contains details of the Calling and Called Parties involved in this call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](#actor) |
| `number`  | In the case of a Webex Calling user, this can be the user's extension, ESN number, or an E164 number. For a PSTN user, this will be an E164 number. |
| `name`    | The full name of the user. This would be the `CallerID` as shown to the user when presenting the call. In the case of a PSTN user, if the name is not available, then the number is used (as is the case with `CallerID`). |

### Actor

This table contains description of type of user involved in the call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `type`    | User (`USER`), Virtual Line (`VIRTUAL_LINE`), or Work Place (`PLACE`) |
| `id`      | Unique identifier of the user |

### Answerer Info

This table contains information about the answering party, it indicates the type of user involved in the call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](#actor) |
| `number`  | In the case of a Webex Calling user, this can be the user's extension, ESN number, or an E164 number. For a PSTN user, this will be an E164 number. This field is populated for cases where the call is answered by a shared line user and includes device owner information. |
| `name`    | The full name of the user. This would be the CallerID as shown to the user when presenting the call. |

### Recording Action

This table contains information about various recording actions applied to the call recording.



| **Field** | **Description** |
| --------- | --------------- |
| `action`  | `PAUSE` or `RESUME` indicates that the recording was paused or resumed. |
| `time`    | The UTC time of the action. |

### Call Activity

This table contains information about call activity. It is a  list of objects that represents the consolidated metadata received at various time-stamps during life of a call (say T0, T1, T2 and so on):



| **Field** | **Description** |
| --------- | --------------- |
| `timeStamp` | The time in UTC when the particular activity was performed. |
| `mediaStreams [array]` | [Media Streams](#media-streams) |
| `participants [array]` | [Participants](#participants) |
| `redirectInfo` | [Redirect Info](#redirect-info) |
| `redirectedCall` | [Redirected Call](#redirected-call) Represents the party from which the call was redirected. This field is populated in cases where a user is transferring a call and, as a result, will likely exit that call. |
| `acd` | [ACD](#acd) This element carries the CallQueue details from where the call was redirected to an agent. |
| `announcementData` | [Announcement Data](#announcement-data) This section carries announcement data (tones, announcements, etc.) that was played and the participant list to whom it was played. |

### Media Streams

This table contains information about the media streams associated with the call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `streamId` | A unique identifier for each stream within a recording session. |
| `mode` | "mixed"/"separate" indicates whether the stream is mixed (both Tx+ Rx) or separate.   NOTE: For the current release, we only support the mixed stream. |
| `mLineIndex` | Represents the `m=` line in SDP to allow recorders to correlate metadata with other information sent in SDP. NOTE: This field is not used in this release. |

### mediaSessions

This table contains information about the mediaSessions associated with each participant, this field is mandatory in metadata version 1.1:



| **Field** | **Description** |
| --------- | --------------- |
| `mediaType` | Represents the type of media. Only “audio” is supported.|
| `mediaContent` | Represents the type of media content. Only “main” is supported.|
| `csi` | Unique 32-bit unsigned integer value. CSI is used to map speaker names in the transcript. The transcript VTT file will contain CSIs and the associated text uttered by that speaker.|

### Connected Party

This table contains information about the connected party in a call. This field is available from metadata version 1.2 and is applicable for Virtual Line, Call Queue, Group Call Pickup, and similar scenarios:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](#actor) |
| `number`  | The phone number or extension of the connected party. |
| `name`    | The display name of the connected party. |

For outbound calls, the connected party is determined based on the identity of the remote connected party. For inbound calls, this refers to the identity of the other party (the caller) that is connected.

### Managed By

This table contains information about the device owner who handled the call. This field is available from metadata version 1.2 for Virtual Line, Shared Line, Call Queue, Group Call Pickup, and similar scenarios:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](#actor) |
| `number`  | The phone number or extension of the device owner. |
| `name`    | The display name of the device owner who handled the call. |

For Virtual Line, Shared Line, Call Queue, Group Call Pickup, and similar scenarios, this indicates the device owner who handled the call.

### Participants

This table contains information about the list of participants associated with the call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](#actor) |
| `aor`     | SIP Address of Record (AoR) |
| `send`    | Points to the unique identifier of the stream to which this participant contributes. The "send" relation is present when the participant is contributing to the stream. If the "send" element is not present, it indicates that the participant is not contributing (e.g., when the participant is in "recvonly" mode). |
| `mediaSessions`     | This field is mandatory in metadata version 1.1 for each participant. This represents the csi information. |
| `number`     | This field carries the participants DN. This can be either E.164 Number or Enterprise-specific numbers (ESN) or Extension. The number field also honors the Webex Calling Connected Line Identity privacy and will hide the identity for cases where privacy is requested. |

### Redirect Info

This table contains information about the call redirection as part of Call Queue and other supplementary service features:



| **Field** | **Description** |
| --------- | --------------- |
| `lastRedirectNumber` | The latest number to which the call was redirected. |
| `origCalledNumber` | The original user, structured the same as [this](#calling-and-called-party). |
| `numOfRedirections` | The number of redirections. |

### Redirected Call

This table contains information about the call redirection due to call transfer feature:



| **Field** | **Description** |
| --------- | --------------- |
| `newExtTrackingId` | Updated `callSessionId` information. |
| `redirectedFromPartyNumber` | Number/SIP AoR of the party who is transferring the call. |
| `redirectedToPartyNumber` | Number/SIP AoR of the user who is the transfer target. |

### ACD

This table contains information about the call redirection and distribution as part of Call Queue feature:



| **Field** | **Description** |
| --------- | --------------- |
| `actor` | [Actor](#PRSConsolidatedMetadataDocumentationand). |
| `acdName` | Call Queue name. |
| `acdNumber->countryCode` | Call Queue country code. |
| `acdNumber->number` | Call Queue extension/number. |

### Announcement Data

This table contains information about the announcement played in this call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `announcementFilename` | Filename. |
| `announcementTimestamp` | UTC time when the announcement is played. |
| `announcementParticipants` | Array of participants. |
| `announcementType` | `USER_LEVEL` (start, pause, resume recording) <br /> `COMPLIANCE` (set when the compliance announcement is enabled). |

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

## Call Queue - Scenarios

1. PSTN Caller: 1001, .
2. Webex Calling Agent: 5050,  (`sip:dtl98hsajj`) (Recording Enabled).
3. Webex Calling Supervisor: 5060 (`sip:x4y6xdsegz`) (Recording Enabled).
4. Call Queue: .
5. PSTN Caller calls the Webex Calling Agent. The Supervisor will perform an action (takeover, barge in, or monitor).

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

## metadata version 1.1 
#### Scenario: Basic Call. Metadata participants included mediaSessions field with csi information for speaker identification feature.

```json

    "metadata": {
        "version": "1.1",
        "timeStamp": "2024-11-06T13: 50: 30Z",
        "mode": "complete",
        "owner": {
            "type": "USER",
            "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3",
            "name": "dave",
            "orgId": "ee8ebeb0-f077-4384-bb50-9de6141c7bac",
            "locale": "en_US",
            "email": "dave@example.com"
        },
        "storageRegion": "US",
        "locationId": "ed009e16-41f4-47d7-9aa6-c44f687612c0",
        "recordingId": "24af194d-b36b-4829-9d61-7159e9fd1d74",
        "callSessionId": "cf1048d3-3da7-4a15-8590-c1176febdc24",
        "session": {
            "startTime": "2024-11-06T13: 50: 30Z"
        },
        "participants": [
            {
                "id": "c4c63c5d-1826-4101-8849-a4c4f6c23109",
                "aor": "sip: kfb1r1cohm@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "dave", //speaker's name
                "number": "6004",//speaker's number or extension
                "actor": {
                    "type": "USER",
                    "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3",
                    "email": "dave@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "b644ee43-a82d-4819-8666-a17ce337e5f1",
                "aor": "sip: 6001@10.155.4.7;user=phone",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "alice", //speaker's name
                "number": "6001", //speaker's extension
                "actor": {
                    "type": "USER",
                    "id": "efcd7974-9356-4f8d-898f-a784a0a81723",
                    "email": "alice@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 77710816
                    }
                ]
            },
            {
                "id": "1711cd6a-75ab-4656-bb44-5b99550a1117",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "system", // IVR announcement play, speaker name showed as "system"
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "e465a741-ba58-4b1e-877e-b6961e088217",
                "aor": "k6sz63bfwn@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "bob",
                "number": "6002",
                "actor": {
                    "type": "USER",
                    "id": "6bb0b081-591f-472e-9b4e-afab20089c6b",
                    "email": "bob@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 706733971
                    }
                ]
            },
            {
                "id": "308de675-5ca2-465f-9996-923e9474b1c4",
                "aor": "gz8ilbortg@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "carol",
                "number": "6003",
                "actor": {
                    "type": "USER",
                    "id": "0a9b1a7e-2063-4d77-a7da-ffb396b0d389",
                    "email": "carol@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "85c18827-fa97-4990-98ba-af74f3674ef7",
                "aor": "izqyme3qip@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "emily",
                "number": "6005",
                "actor": {
                    "type": "USER",
                    "id": "9650d89e-f0bd-4117-86e4-efce06fea374",
                    "email": "emily@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 221319636
                    }
                ]
            }
        ],
        "mediaStreams": [
            {
                "streamId": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "mode": "mixed",
                "mLineIndex": "0"
            }
        ],
        "extensionData": {
            "recordingType": "alwaysON",
            "userId": "kfb1r1cohm@64941297.int10.bcld.webex.com",
            "callId": "callhalf-101170306: 0",
            "callData": {
                "type": "origCall",
                "callingParty": {
                    "actor": {
                        "type": "USER",
                        "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3"
                    },
                    "number": "6004",
                    "name": "dave"
                },
                "calledParty": {
                    "actor": {
                        "type": "USER",
                        "id": "efcd7974-9356-4f8d-898f-a784a0a81723"
                    },
                    "number": "6001",
                    "name": "alice"
                },
                "dialedDigits": "sip: 6001@10.155.4.7"
            }
        }
    }
```

#### Scenario: Outgoing PSTN call. Metadata participants included mediaSessions field with csi information for speaker identification feature.

```json

 {
  "id": "029cf270-13f6-46ab-ba31-37dc810aa0b2",
  "orgId": "9b766f58-6cfc-473a-871e-a55459829cde",
  "ownerId": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
  "ownerType": "USER",
  "ownerName": "carol",
  "ownerEmail": "carol@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "029cf270-13f6-46ab-ba31-37dc810aa0b2",
    "locationId": "4907ed26-0fb4-47ce-be9d-4e1ac3ce1afb",
    "callSessionId": "795c5ef8-f871-48e7-afcb-842007281226",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
        "email": null
      },
      "number": "",
      "name": "carol"
    },
    "calledParty": {
      "actor": null,
      "number": "",
      "name": ""
    },
    "callId": "callhalf-109517238:0",
    "session": {
      "startTime": "2024-11-27T07:55:49Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-11-27T07:55:49Z",
        "mediaStreams": [
          {
            "streamId": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "a41de2bc-abde-4b7e-a0af-7c19c79a7cd6",
            "name": "carol",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
              "email": "carol@example.com"
            },
            "aor": "sip:dcrvlqxti7@******",
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
          },
          {
            "id": "4d64c490-d40b-4aca-856f-9e5cf8ab196e",
            "name": "",
            "number": "",
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
          },
          {
            "id": "494a6b6a-40ee-4842-83c7-d2be02d5a649",
            "name": "system",
            "number": null,
            "actor": null,
            "aor": null,
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
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

#### Scenario: Call hold-resume

```json
{
  "id": "436ba427-2ea2-46ab-9e0c-f6c156189bf0",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "IN",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "436ba427-2ea2-46ab-9e0c-f6c156189bf0",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "ed9ae7c9-5cc1-4e44-9384-fa4c8ccf699c",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
      },
      "number": "8001",
      "name": "bob"
    },
    "callId": "callhalf-73322436:0",
    "session": {
      "startTime": "2025-01-09T02:43:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:43:00Z",
        "mediaStreams": [
          {
            "streamId": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "1a62c69a-87ab-4e49-a999-429a5fde5c05",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "225001639"
              }
            ]
          },
          {
            "id": "f4a23718-a02b-49cf-8c50-4032f6888c63",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "sip:8001@X.X.X.X;user=phone",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "9895bcee-c89e-4e44-9347-12a4cee6ab8e",
            "name": "system",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ]
      }
    ]
  }
}
```

#### Scenario: Blind call transfer

```json


{
  "id": "f53e4f4b-122c-41e5-82f2-907b18ecec4b",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
  "ownerType": "USER",
  "ownerName": ". carol",
  "ownerEmail": "carol@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "f53e4f4b-122c-41e5-82f2-907b18ecec4b",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "61afe5ef-3d3e-477f-86a0-4584fc81775d",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "8000",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2"
      },
      "number": "7002",
      "name": "carol"
    },
    "callId": "callhalf-73323092:0",
    "session": {
      "startTime": "2025-01-09T02:44:27Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:44:27Z",
        "mediaStreams": [
          {
            "streamId": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "4abf7d1b-9fa3-4334-a281-1b5ee8600e5e",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:o5o1guuv31@******",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "f306ac2b-4629-4336-9f04-ce2058d76650",
            "name": "alice",
            "number": "8000",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:8000@X.X.X.X;user=phone",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "c919c3a6-86f2-4a17-b37240",
            "name": "system",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "7002",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
            },
            "number": ""
          },
          "numOfRedirections": 1
        }
      }
    ]
  }
}
```

#### Scenario: Consult call transfer

```json

{
  "id": "ec7315eb-f5a7-4c49-be0d-f510ead3212b",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "ec7315eb-f5a7-4c49-be0d-f510ead3212b",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "61afe5ef-3d3e-477f-86a0-4584fc81775d",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
      },
      "number": "8001",
      "name": "bob"
    },
    "callId": "callhalf-73322940:0",
    "session": {
      "startTime": "2025-01-09T02:44:06Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:44:06Z",
        "mediaStreams": [
          {
            "streamId": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "bc631506-a93d-4fb3-a420-74df70cff9a0",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "727981502"
              }
            ]
          },
          {
            "id": "4d1671e2-bcd9-4ade-9a3b-2b151db431ed",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "sip:8001@X.X.X.X;user=phone",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "bbf1e699-454a-469f-b1f8-b9d164b45b25",
            "name": "system",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "ea95a2d2-7c44-4f5e-bc6f-5c024e541ccd",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone"
          },
          {
            "id": "82e4d767-f117-4823-9933-16d8fa473365",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone",
            "send": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ],
        "redirectedCall": {
          "redirectedFromPartyNumber": "8001",
          "redirectedToPartyNumber": "sip:7002@X.X.X.X;user=phone"
        }
      }
    ]
  }
}
```
#### Scenario: Conference call

```json
{
  "id": "726bbaef-321c-4a41-8ec8-36d901a09f49",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "726bbaef-321c-4a41-8ec8-36d901a09f49",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "55e45a6c-d42b-4bb7-87f1-0808f4a66156",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2"
      },
      "number": "7002",
      "name": "carol"
    },
    "callId": "callhalf-73323568:1",
    "session": {
      "startTime": "2025-01-09T02:45:51Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:45:51Z",
        "mediaStreams": [
          {
            "streamId": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "4110698b-3267-46d6-b6eb-7177a0ecd07e",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "2f6e4899-29a2-4a2c-8f58-ee0c24dd63e9",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "0914ed1f-45a9-49f8-8c70-effe271a0e15",
            "name": "system",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "a8224e4e-3583-4a36-a7f1-f9db8e042f1f",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "wgqwgarksy@******",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ]
      }
    ]
  }
}
```

## metadata version 1.2

Metadata version 1.2 introduces two new fields in `serviceData`: `connectedParty` and `managedBy`. The following samples demonstrate these fields across various calling scenarios.

`answererInfo` is deprecated starting with metadata version `1.2` and should not be expected in version `1.2` payloads.



#### Scenario: Outbound Call with Connected Party

This example shows an outbound call where the `connectedParty` field captures the identity of the remote connected party.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8wYjFhNmQ3MC0yMDk2LTRkMTctOTgxZS0yMjdkMjNlMTkzMmE",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xYjU2MDVjYS1lMjMwLTQzMzAtYjVhYy1hZDEwMmNhMTg4NjA",
  "ownerType": "USER",
  "ownerName": "Test User",
  "ownerEmail": "testuser@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "0b1a6d70-2096-4d17-981e-227d23e1932a",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "f8a2b3c4-d5e6-7890-abcd-ef1234567890",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xYjU2MDVjYS1lMjMwLTQzMzAtYjVhYy1hZDEwMmNhMTg4NjA",
        "email": "testuser@example.com"
      },
      "number": "5001",
      "name": "Test User"
    },
    "calledParty": {
      "actor": null,
      "number": "+14085551234",
      "name": ""
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "External User"
    },
    "callId": "callhalf-123456789:0",
    "session": {
      "startTime": "2025-03-15T10:30:00Z",
      "stopTime": "2025-03-15T10:35:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Inbound Call with Connected Party

This example shows an inbound call where the `connectedParty` field refers to the identity of the caller that is connected.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8xYTJiM2M0ZC01ZTZmLTdhOGItOWMwZC1lZjEyMzQ1Njc4OTA",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8yYzM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
  "ownerType": "USER",
  "ownerName": "Alice Smith",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "1a2b3c4d-5e6f-7a8b-9c0d-ef1234567890",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085559876",
      "name": "External Caller"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8yYzM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
        "email": "alice@example.com"
      },
      "number": "5002",
      "name": "Alice Smith"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085559876",
      "name": "External Caller"
    },
    "callId": "callhalf-987654321:0",
    "session": {
      "startTime": "2025-03-15T11:00:00Z",
      "stopTime": "2025-03-15T11:10:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Shared Line with Managed By

This example demonstrates the `managedBy` field for a shared line scenario, indicating the device owner who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
  "ownerType": "USER",
  "ownerName": "Bob Johnson",
  "ownerEmail": "bob@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "3d4e5f6g-7h8i-9j0k-1l2-m3n4o5p6q7r8",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS80ZTVmNmc3aC04aTlqLTBrMWwtMm0zbi00bzVwNnE3cjhzOQ",
        "email": "carol@example.com"
      },
      "number": "5003",
      "name": "Carol Davis"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
        "email": "bob@example.com"
      },
      "number": "5004",
      "name": "Bob Johnson"
    },
    "connectedParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS80ZTVmNmc3aC04aTlqLTBrMWwtMm0zbi00bzVwNnE3cjhzOQ",
        "email": "carol@example.com"
      },
      "number": "5003",
      "name": "Carol Davis"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81ZjZnN2g4aS05ajBrLTFsMm0tM240by01cDZxN3I4czl0MA",
        "email": "manager@example.com"
      },
      "number": "5005",
      "name": "Line Manager"
    },
    "callId": "callhalf-112233445:0",
    "session": {
      "startTime": "2025-03-15T14:00:00Z",
      "stopTime": "2025-03-15T14:15:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Virtual Line with Managed By

This example shows a virtual line scenario where `managedBy` indicates the device owner who handled the call on behalf of the virtual line.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1ZJUlRVQUxfTElORS82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0",
  "ownerType": "VIRTUAL_LINE",
  "ownerName": "Sales Hotline",
  "ownerEmail": "sales@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "6f7g8h9i-0j1k-2l3m-4n5o-6p7q8r9s0t",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "c3d4e5f6-a7b8-9012-cdef-345678901234",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085557777",
      "name": "Customer"
    },
    "calledParty": {
      "actor": {
        "type": "VIRTUAL_LINE",
        "id": "Y2lzY29zcGFyazovL3VzL1ZJUlRVQUxfTElORS82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0"
      },
      "number": "8001",
      "name": "Sales Hotline"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085557777",
      "name": "Customer"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83aDhpOWowLTFrMmwtM200bi01bzZwN3E4cjlzMHQxdTI",
        "email": "salesrep@example.com"
      },
      "number": "5010",
      "name": "Sales Representative"
    },
    "callId": "callhalf-556677889:0",
    "session": {
      "startTime": "2025-03-15T15:30:00Z",
      "stopTime": "2025-03-15T15:45:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Call Queue with Agent as Recording Owner

This example shows a call queue scenario where a call is routed to a call queue and answered by an agent. The recording owner is the agent, and `managedBy` indicates the agent who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
  "ownerType": "USER",
  "ownerName": "Agent Smith",
  "ownerEmail": "agent.smith@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "9a0b1c2d-3e4f-5a6b-7c8d-9e0f1a2b3c4d",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "d4e5f6a7-b8c9-0123-defg-456789012345",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "Customer"
    },
    "calledParty": {
      "actor": {
        "type": "CALL_QUEUE",
        "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
      },
      "number": "8000",
      "name": "Support Queue"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "Customer"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
        "email": "agent.smith@example.com"
      },
      "number": "6001",
      "name": "Agent Smith"
    },
    "callId": "callhalf-998877665:0",
    "session": {
      "startTime": "2025-03-15T16:00:00Z",
      "stopTime": "2025-03-15T16:12:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-03-15T16:00:00Z",
        "mediaStreams": [
          {
            "streamId": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "p1a2b3c4-d5e6-f7a8-b9c0-d1e2f3a4b5c6",
            "name": "Agent Smith",
            "number": "6001",
            "actor": {
              "type": "USER",
              "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
              "email": "agent.smith@example.com"
            },
            "aor": "sip:agentsmith@******",
            "send": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "123456789"
              }
            ]
          },
          {
            "id": "p2b3c4d5-e6f7-a8b9-c0d1-e2f3a4b5c6d7",
            "name": "Customer",
            "number": "+14085551234",
            "actor": null,
            "aor": "sip:+14085551234@X.X.X.X;user=phone",
            "send": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "987654321"
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "6001",
          "origCalledNumber": {
            "actor": {
              "type": "CALL_QUEUE",
              "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
            },
            "number": "8000"
          },
          "numOfRedirections": 1
        },
        "acd": {
          "actor": {
            "type": "CALL_QUEUE",
            "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
          },
          "acdName": "Support Queue",
          "acdNumber": "8000"
        },
        "announcementData": null
      }
    ]
  }
}
```

#### Scenario: PSTN Caller to Call Queue with Call Queue as Recording Owner

This example shows a PSTN caller calling a Call Queue. The recording owner is the Call Queue, and `managedBy` indicates the agent who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8xMjM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q",
  "ownerType": "CALL_QUEUE",
  "ownerName": "Customer Support Queue",
  "ownerEmail": null,
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "12345678-abcd-ef12-3456-7890abcdef12",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "e5f6a7b8-c9d0-1234-efgh-567890123456",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085559999",
      "name": ""
    },
    "calledParty": {
      "actor": {
        "type": "CALL_QUEUE",
        "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
      },
      "number": "8000",
      "name": "Customer Support Queue"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085559999",
      "name": ""
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hZ2VudDEyMzQ1Njc4OTBhYmNkZWYxMjM0",
        "email": "agent.johnson@example.com"
      },
      "number": "6010",
      "name": "Agent Johnson"
    },
    "callId": "callhalf-445566778:0",
    "session": {
      "startTime": "2025-03-16T09:00:00Z",
      "stopTime": "2025-03-16T09:15:30Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-03-16T09:00:00Z",
        "mediaStreams": [
          {
            "streamId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "p1-agent-johnson-12345",
            "name": "Agent Johnson",
            "number": "6010",
            "actor": {
              "type": "USER",
              "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hZ2VudDEyMzQ1Njc4OTBhYmNkZWYxMjM0",
              "email": "agent.johnson@example.com"
            },
            "aor": "sip:agentjohnson@******",
            "send": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "111222333"
              }
            ]
          },
          {
            "id": "p2-pstn-caller-67890",
            "name": "",
            "number": "+14085559999",
            "actor": null,
            "aor": "sip:+14085559999@X.X.X.X;user=phone",
            "send": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "444555666"
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "6010",
          "origCalledNumber": {
            "actor": {
              "type": "CALL_QUEUE",
              "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
            },
            "number": "8000"
          },
          "numOfRedirections": 1
        },
        "acd": {
          "actor": {
            "type": "CALL_QUEUE",
            "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
          },
          "acdName": "Customer Support Queue",
          "acdNumber": "8000"
        },
        "announcementData": null
      }
    ]
  }
}
```
