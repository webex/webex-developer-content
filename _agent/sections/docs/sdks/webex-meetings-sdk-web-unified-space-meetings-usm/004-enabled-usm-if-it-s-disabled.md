---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Enabled USM if It's Disabled
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-unified-space-meetings-usm.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites for USM](002-prerequisites-for-usm.md)

## Article introduction

Webex Meeting today has three distinct meeting experiences: Personal Meeting Rooms (PMR), Scheduled Meetings, and Space Meetings. Each of those meeting types has distinct experiences. Unified Space Meetings (USM) consolidates the experiences of Space Meetings with Webex Meetings and melds them together.

This article explains how to enable USM, how to start ad-hoc meetings, including information on password and captcha support.

## Selected section

## Enabled USM if It's Disabled

To toggle USM on or off:

```js
webex.meetings._toggleUnifiedMeetings(changeState);
```



|                  |                                     |
| ---------------- | ----------------------------------- |
| **Asynchronous** | No                                  |
| **Parameters**   | `changeState<Boolean (true / false)>` |
| **Returns**      | undefined                           |

You can also change the configuration by toggling the following values:

```js
Meetings :{
 experimental: {
      enableUnifiedMeetings: false,
      enableAdhocMeetings: false
    }
  }
```
