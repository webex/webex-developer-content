---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Join a Meeting
- The joinOptions Object
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-join-a-meeting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Joining a meeting using the Webex Meetings Web SDK allows you to participate in video conferences. This article guides you through the process of joining a meeting and covers various additional scenarios, including joining with or without media, configuring audio and video settings, and screen sharing.

## Parent context

## Join a Meeting

Once you have a `Meeting` object, you can join the meeting using the `join()` method:

```js
const join = await meeting.join(joinOptions);
```

You can specify options via a `joinOptions` object, including PSTN, video, and screensharing:



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td>
        <strong>Asynchronous</strong>
      </td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>
        <strong>Parameters</strong>
      </td>
      <td>
        
          <table>
            <thead>
              <tr>
                <th><strong>Name</strong></th>
                <th><strong>Description</strong></th>
                <th><strong>Type</strong></th>
                <th><strong>Mandatory</strong></th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>joinOptions</code></td>
                <td>
                  A configurable options object for joining a meeting.
                </td>
                <td><strong>JoinOptions</strong></td>
                <td>No</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        <strong>Returns</strong>
      </td>
      <td colspan="1">
        Promise&lt;JoinResponse&gt;
      </td>
    </tr>
  </tbody>
</table>

The `join()` method returns a `JoinResponse` object containing comprehensive details about the meeting.

## Selected section

### The joinOptions Object

The `joinOptions` object determines how a participant joins a meeting:



| **Attribute Name** | **Description** | **Type** | **Optional** |
| --- | --- | --- | --- |
| `resourceId` | `resourceId` of the paired device if joining with a Device. | **String** | Yes |
| `moveToResource` | Moves the meeting to the paired device, if `true`. | **Boolean** | Yes |
| `pin` | PIN of the Meeting room, if you're joining as a host. | **String** | Yes |
| `moderator` | Indicate if you are joining as a moderator/host. | **Boolean** | Yes |
| `meetingQuality` | Customize meeting video quality settings. | **Object** | Yes |
| `meetingQuality.local` | Set the local video quality. Valid values are: "360p", "480p", "720p", and "1080p". | **String** | Yes |
| `meetingQuality.remote` | Set remote video quality. Valid values are: "LOW", "MEDIUM", and "HIGH". | **String** | Yes |
| `rejoin` | Allow or disallow rejoining the meeting. | **Boolean** | Yes |

Here's a sample `joinOptions` object:

```javascript
const joinOptions = {
  pin: '123456',
  moderator: false,
  moveToResource: false,
  resourceId: '31c4a552-4167-49ef-8034-c8dc8c5de76f',
  receiveTranscription: false,
  meetingQuality: {
    local: '720p',
    remote: 'HIGH'
  },
  rejoin: false
};
```
