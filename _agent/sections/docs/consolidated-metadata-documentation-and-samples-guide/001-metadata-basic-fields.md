---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Metadata Basic Fields
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

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
| `serviceData`     | [Service Data](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#service-data).                                                                        |

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
| `answererInfo`            | [Answerer Info](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#answerer-info). Optional element populated for cases like Shared lines and contains device owner information of the user who answered the call. |
| `recordingActions`        | [Recording Action](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#recording-actions). Optional element added when recording pause/resume is done within a recording session. |
| `callActivity (list)`     | [Call Activity](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#call-activity). Optional element that gives additional information about activities that happened during the call (e.g., transfer, redirected party information, announcement details, etc.). |

### Calling and Called Party

This table contains details of the Calling and Called Parties involved in this call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#actor) |
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
| `actor`   | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#actor) |
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
| `mediaStreams [array]` | [Media Streams](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#media-streams) |
| `participants [array]` | [Participants](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#participants) |
| `redirectInfo` | [Redirect Info](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#redirect-info) |
| `redirectedCall` | [Redirected Call](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#redirected-call) Represents the party from which the call was redirected. This field is populated in cases where a user is transferring a call and, as a result, will likely exit that call. |
| `acd` | [ACD](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#acd) This element carries the CallQueue details from where the call was redirected to an agent. |
| `announcementData` | [Announcement Data](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#announcement-data) This section carries announcement data (tones, announcements, etc.) that was played and the participant list to whom it was played. |

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
| `actor`   | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#actor) |
| `number`  | The phone number or extension of the connected party. |
| `name`    | The display name of the connected party. |

For outbound calls, the connected party is determined based on the identity of the remote connected party. For inbound calls, this refers to the identity of the other party (the caller) that is connected.

### Managed By

This table contains information about the device owner who handled the call. This field is available from metadata version 1.2 for Virtual Line, Shared Line, Call Queue, Group Call Pickup, and similar scenarios:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#actor) |
| `number`  | The phone number or extension of the device owner. |
| `name`    | The display name of the device owner who handled the call. |

For Virtual Line, Shared Line, Call Queue, Group Call Pickup, and similar scenarios, this indicates the device owner who handled the call.

### Participants

This table contains information about the list of participants associated with the call recording:



| **Field** | **Description** |
| --------- | --------------- |
| `actor`   | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#actor) |
| `aor`     | SIP Address of Record (AoR) |
| `send`    | Points to the unique identifier of the stream to which this participant contributes. The "send" relation is present when the participant is contributing to the stream. If the "send" element is not present, it indicates that the participant is not contributing (e.g., when the participant is in "recvonly" mode). |
| `mediaSessions`     | This field is mandatory in metadata version 1.1 for each participant. This represents the csi information. |
| `number`     | This field carries the participants DN. This can be either E.164 Number or Enterprise-specific numbers (ESN) or Extension. The number field also honors the Webex Calling Connected Line Identity privacy and will hide the identity for cases where privacy is requested. |

### Redirect Info

This table contains information about the call redirection as part of Call Queue and other supplementary service features:



| **Field** | **Description** |
| --------- | --------------- |
| `lastRedirectNumber` | The latest number to which the call was redirected. |
| `origCalledNumber` | The original user, structured the same as [this](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#calling-and-called-party). |
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
| `actor` | [Actor](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide#PRSConsolidatedMetadataDocumentationand). |
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
