---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Meeting Types
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for USM](002-prerequisites-for-usm.md)

## Article introduction

Webex Meeting today has three distinct meeting experiences: Personal Meeting Rooms (PMR), Scheduled Meetings, and Space Meetings. Each of those meeting types has distinct experiences. Unified Space Meetings (USM) consolidates the experiences of Space Meetings with Webex Meetings and melds them together.

This article explains how to enable USM, how to start ad-hoc meetings, including information on password and captcha support.

## Selected section

## Webex Meeting Types

Webex meetings can be broadly classified as:

1. **Webex Meetings**
   1. *Scheduled Webex Meetings* - The meeting is created first and then the meeting information such as the meeting ID, pass code, and unique meeting link is sent to the **invitees**.
   1. *PMR (personal meeting room or "instant meeting")* - A meeting with a static URL that can be attached to a meeting schedule as well as sent out as a message for anyone to join.
1. **Space Meetings**
   1. *Scheduled Space Meetings* - The meeting is created first and then the meeting information such as the meeting ID, pass code, and unique meeting link is sent to the **members of the space**.
   1. *Ad-hoc Space Meetings* - The meeting can be started instantly from a team space, without any pre-scheduled meeting links. Although these meetings are instant and do not have a meeting ID or URL when they're started, Webex creates both which can be obtained via the Meeting Info API.
