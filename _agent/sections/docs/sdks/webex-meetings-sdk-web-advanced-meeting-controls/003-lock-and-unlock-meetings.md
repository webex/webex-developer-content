---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Lock and Unlock Meetings
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

## Lock and Unlock Meetings

When you lock a meeting, no other participants can join unless you admit them. Only the host of a meeting can lock and unlock meetings.

### Lock a Meeting

To lock a meeting, use the `Meeting` object's `lockMeeting()` method:

```javascript
await meeting.lockMeeting();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Unlocking a meeting

To unlock a meeting, use the `Meeting` object's `unlockMeeting()` method:

```javascript
await meeting.unlockMeeting();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | Promise<undefined> |
