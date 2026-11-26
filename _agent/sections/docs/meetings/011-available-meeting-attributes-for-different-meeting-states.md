---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Available Meeting Attributes for Different Meeting States
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md) [Restrictions on Updating a Meeting](015-restrictions-on-updating-a-meeting.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Available Meeting Attributes for Different Meeting States

The table below lists which meeting attributes are available for different meeting states when the meeting type is `meetingSeries`:



| Attributes | state=active | state=inProgress | state=expired |
|---|---|---|---|
| `id` | Yes | Yes | Yes |
| `meetingNumber` | Yes | Yes | Yes |
| `title` | Yes | Yes | Yes |
| `agenda` | Yes | Yes | Yes |
| `password` | Yes | Yes | Yes |
| `phoneAndVideoSystemPassword` | Yes | Yes | Yes |
| `meetingType` | Yes | Yes | Yes |
| `state` | Yes | Yes | Yes |
| `isModified` | No | No | No |
| `timezone` | Yes | Yes | Yes |
| `start` | Yes | Yes | Yes |
| `end` | Yes | Yes | Yes |
| `recurrence` | Yes | Yes | Yes |
| `hostUserId` | Yes | Yes | Yes |
| `hostDisplayName` | Yes | Yes | Yes |
| `hostEmail` | Yes | Yes | Yes |
| `hostKey` | Yes | Yes | Yes |
| `siteUrl` | Yes | Yes | Yes |
| `webLink` | Yes | Yes | Yes |
| `sipAddress` | Yes | Yes | Yes |
| `dialInIpAddress` | Yes | Yes | Yes |
| `enabledAutoRecordMeeting` | Yes | Yes | Yes |
| `allowAnyUserToBeCoHost` | Yes | Yes | Yes |
| `enabledJoinBeforeHost` | Yes | Yes | Yes |
| `enableConnectAudioBeforeHost` | Yes | Yes | Yes |
| `joinBeforeHostMinutes` | Yes | Yes | Yes |
| `excludePassword` | Yes | Yes | Yes |
| `publicMeeting` | Yes | Yes | Yes |
| `reminderTime` | Yes | Yes | Yes |
| `unlockedMeetingJoinSecurity` | Yes | Yes | Yes |
| `enableAutomaticLock` | Yes | Yes | Yes |
| `automaticLockMinutes` | Yes | Yes | Yes |
| `allowFirstUserToBeCoHost` | Yes | Yes | Yes |
| `allowAuthenticatedDevices` | Yes | Yes | Yes |
| `telephony` | Yes | Yes | Yes |
| `meetingOptions` | Yes | Yes | Yes |
| `attendeePrivileges` | Yes | Yes | Yes |
| `registration` | Yes | Yes | No |
| `integrationTags` | Yes | Yes | Yes |
| `scheduledType` | Yes | Yes | Yes |
| `simultaneousInterpretation` | Yes | Yes | Yes |
| `enabledBreakoutSessions` | Yes | Yes | Yes |
| `links` | Yes | Yes | Yes |
| `trackingCodes` | Yes | Yes | Yes |
| `audioConnectionOptions` | Yes | Yes | Yes |

The table below lists which meeting attributes are available for different meeting states when the meeting type is `scheduledMeeting`:



| Attributes | state=scheduled | state=ready | state=ended | state=missed |
|---|---|---|---|---|
| `id` | Yes | Yes | Yes | Yes |
| `meetingNumber` | Yes | Yes | Yes | Yes |
| `title` | Yes | Yes | Yes | Yes |
| `agenda` | Yes | Yes | Yes | Yes |
| `password` | Yes | Yes | Yes | Yes |
| `phoneAndVideoSystemPassword` | Yes | Yes | Yes | Yes |
| `meetingType` | Yes | Yes | Yes | Yes |
| `state` | Yes | Yes | Yes | Yes |
| `isModified` | Yes | Yes | Yes | Yes |
| `timezone` | Yes | Yes | Yes | Yes |
| `start` | Yes | Yes | Yes | Yes |
| `end` | Yes | Yes | Yes | Yes |
| `recurrence` | No | No | No | No |
| `hostUserId` | Yes | Yes | Yes | Yes |
| `hostDisplayName` | Yes | Yes | Yes | Yes |
| `hostEmail` | Yes | Yes | Yes | Yes |
| `hostKey` | Yes | Yes | Yes | Yes |
| `siteUrl` | Yes | Yes | Yes | Yes |
| `webLink` | Yes | Yes | Yes | Yes |
| `sipAddress` | Yes | Yes | Yes | Yes |
| `dialInIpAddress` | Yes | Yes | Yes | Yes |
| `enabledAutoRecordMeeting` | Yes | Yes | Yes | Yes |
| `allowAnyUserToBeCoHost` | Yes | Yes | Yes | Yes |
| `enabledJoinBeforeHost` | Yes | Yes | Yes | Yes |
| `enableConnectAudioBeforeHost` | Yes | Yes | Yes | Yes |
| `joinBeforeHostMinutes` | Yes | Yes | Yes | Yes |
| `excludePassword` | Yes | Yes | Yes | Yes |
| `publicMeeting` | Yes | Yes | Yes | Yes |
| `reminderTime` | Yes | Yes | Yes | Yes |
| `unlockedMeetingJoinSecurity` | Yes | Yes | Yes | Yes |
| `enableAutomaticLock` | Yes | Yes | Yes | Yes |
| `automaticLockMinutes` | Yes | Yes | Yes | Yes |
| `allowFirstUserToBeCoHost` | Yes | Yes | Yes | Yes |
| `allowAuthenticatedDevices` | Yes | Yes | Yes | Yes |
| `telephony` | Yes | Yes | Yes | Yes |
| `meetingOptions` | Yes | Yes | Yes | Yes |
| `attendeePrivileges` | Yes | Yes | Yes | Yes |
| `registration` | N/A | Yes | No | No |
| `integrationTags` | Yes | Yes | Yes | Yes |
| `scheduledType` | Yes | Yes | Yes | Yes |
| `simultaneousInterpretation` | Yes | Yes | Yes | Yes |
| `enabledBreakoutSessions` | Yes | Yes | Yes | Yes |
| `links` | Yes | Yes | Yes | Yes |
| `trackingCodes` | Yes | Yes | Yes | Yes |
| `audioConnectionOptions` | Yes | Yes | Yes | Yes |

The table below lists which meeting attributes are available for different meeting states when the meeting type is `meeting`:



| Attributes | state=lobby | state=inProgress | state=ended |
|---|---|---|---|
| `id` | Yes | Yes | Yes |
| `meetingNumber` | Yes | Yes | No |
| `title` | Yes | Yes | Yes |
| `agenda` | Yes | Yes | Yes |
| `password` | No | Yes | No |
| `phoneAndVideoSystemPassword` | No | Yes | No |
| `meetingType` | Yes | Yes | Yes |
| `state` | Yes | Yes | Yes |
| `isModified` | No | No | No |
| `timezone` |Yes | Yes | Yes |
| `start` | Yes | Yes | Yes |
| `end` | No | No | Yes |
| `recurrence` | No | No | No |
| `hostUserId` | Yes | Yes | Yes |
| `hostDisplayName` | Yes | Yes | Yes |
| `hostEmail` | Yes | Yes | Yes |
| `hostKey` | No | Yes | No |
| `siteUrl` | Yes | Yes | Yes |
| `webLink` | Yes | Yes | Yes |
| `sipAddress` | No | Yes | No |
| `dialInIpAddress` | No | Yes | No |
| `enabledAutoRecordMeeting` | No | Yes | No |
| `allowAnyUserToBeCoHost` | No | Yes | No |
| `enabledJoinBeforeHost` | No | Yes | No |
| `enableConnectAudioBeforeHost` | No | Yes | No |
| `joinBeforeHostMinutes` | No | Yes | No |
| `excludePassword` | No | Yes | No |
| `publicMeeting` | No | Yes | No |
| `reminderTime` | No | Yes | No |
| `unlockedMeetingJoinSecurity` | No | Yes | No |
| `enableAutomaticLock` | No | Yes | No |
| `automaticLockMinutes` | No | Yes | No |
| `allowFirstUserToBeCoHost` | No | Yes | No |
| `allowAuthenticatedDevices` | No | Yes | No |
| `telephony` | No | Yes | No |
| `meetingOptions` | No | Yes | No |
| `attendeePrivileges` | No | Yes | No |
| `registration` | Yes | Yes | No |
| `integrationTags` | Yes | Yes | Yes |
| `scheduledType` | Yes | Yes | Yes |
| `simultaneousInterpretation` | No | Yes | No |
| `enabledBreakoutSessions` | No | Yes | No |
| `links` | No | Yes | No |
| `trackingCodes` | No | Yes | No |
| `audioConnectionOptions` | No | Yes | No |
