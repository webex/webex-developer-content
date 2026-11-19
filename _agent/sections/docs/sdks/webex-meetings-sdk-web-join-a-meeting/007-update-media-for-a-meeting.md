---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Join a Meeting
- Update Media for a Meeting
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

### Update Media for a Meeting

At any time in the meeting, you can remove or add additional media streams using the following methods. While updating a media of the same type (e.g. camera stream), first unpublish the media streams before publishing the new streams.

#### Add Media Stream

If we already have media added to a meeting, we can add more streams by using the publishStreams() method as follows.

```js
await meeting.publishStreams({camera: cameraStream}));
```



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
                <td><code>localStreams</code></td>
                <td>
                  A configurable options object for joining a meeting.
                </td>
                <td><strong>LocalStreams</strong></td>
                <td>Yes</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        Returns
      </td>
      <td colspan="1">Promise&lt;undefined&gt;</td>
    </tr>
  </tbody>
</table>

#### Remove a Media Stream

The `streamsToUnpublish()` method is used to remove a media stream from the meeting.



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
                <td><code>streams</code></td>
                <td>
                    An array of all the streams that need to be unpublished.
                </td>
                <td>
                  <strong>LocalStream[]</strong>
                </td>
                <td>Yes</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        Returns
      </td>
      <td colspan="1">Promise&lt;undefined&gt;</td>
    </tr>
  </tbody>
</table>

To remove media streams:

```js
const streamsToUnpublish = [];

if (localMedia.screenShare.audio) {
  streamsToUnpublish.push(screenShare.audio);
}
if (localMedia.screenShare.video) {
  streamsToUnpublish.push(screenShare.video);
}

if (streamsToUnpublish.length) {
  await meeting.unpublishStreams(streamsToUnpublish);
}
```

#### Join a Meeting with Media

The `joinWithMedia()` method lets you join a meeting and add media in a single operation.



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
        <strong>Options</strong>
        
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
                <td>
                  <a href="#the-joinoptions-object">JoinOptions</a>
                </td>
                <td>No</td>
              </tr>
              <tr>
                <td colspan="1"><code>mediaOptions</code></td>
                <td colspan="1">
                  A configurable options object for setting up media.
                </td>
                <td colspan="1">
                  <a href="#the-addmedia-method">AddMediaOptions</a>
                </td>
                <td colspan="1">No</td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        Returns
      </td>
      <td colspan="1">Promise&lt;JoinResponse&gt;</td>
    </tr>
  </tbody>
</table>

Join a meeting using `joinOptions` and `mediaOptions`:

```js
const options = {
  joinOptions: {
    pin: '123456',
    moderator: false
  },
  mediaOptions: {
    localStreams: {
      microphone: microphoneStream,
      camera: cameraStream
    },
    audioEnabled: true,
    videoEnabled: true,
    shareVideoEnabled: true,
    shareAudioEnabled: false,
    additionalMediaOptions: {
      sendVideo: true,
      receiveVideo: true,
      sendAudio: true,
      receiveAudio: true
    }
  }
};

await meeting.joinWithMedia(options);
```


> **Info**
>
> Screen share audio is unavailable for single stream, transcoded meetings and is only available in a multi-stream setting.





> **Info**
>
> If the participant is challenged with a PIN/password or made to wait in the lobby, media has to be set up once the participant is added to the meeting. You can then listen to meeting events ([meeting:self:guestAdmitted](https://webex.github.io/webex-js-sdk/api/#meetingeventmeetingselfguestadmitted)) and perform subsequent operations like adding media.



Here are the various scenarios in which the `joinOptions` object can vary:



| **Scenario** | **Description** | **Parameter** **Requirement** |
| --- | --- | --- |
| A | Joining your personal meeting room. | NA |
| B | Joining someone else's personal meeting room. | Use the host pin to join someone else's PMR as a host and assume host privilegs in the meeting. |
| C | Joining an unclaimed personal meeting room. | The join will throw an error in this scenario when you try to join without any options. |
| D | Joining in any other way (SIP, PSTN, `conversationUrl`, link, etc.) | Only specify `resourceId` if joining with a device. |
