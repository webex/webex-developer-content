---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Screen Recording
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-advanced-meeting-controls.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes the advanced meeting controls available in the Webex Web SDK for meetings.

## Selected section

## Screen Recording

Once a meeting is [created](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction#create-a-meeting) and [joined](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting), the screen recording controls can be initialized. Only the host of a meeting has the capability to record the screen and manage its controls. Scroll to the end of this page to learn how to determine the current user's role.

### Start a Recording

To start a recording, use the `Meeting` object's `startRecording()` method:

```javascript
await meeting.startRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Pause a Recording

For a recording in process, pause the recording using the `Meeting` object's `pauseRecording()` method:

```javascript
await meeting.pauseRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Resume a Recording

To resume recording, use the `Meeting` object's `resumeRecording()` method:

```javascript
await meeting.resumeRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |

### Stop a Recording

To stop recording, use the `Meeting` object's `stopRecording()` method:

```javascript
await meeting.stopRecording();
```



|                  |                      |
| ---------------- | -------------------- |
| **Asynchronous** | Yes                  |
| **Parameters**   | None                 |
| **Returns**      | `Promise<undefined>` |
