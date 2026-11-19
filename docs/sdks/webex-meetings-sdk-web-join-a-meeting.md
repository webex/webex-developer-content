---
type: Guide
title: Web Meetings SDK | Join a Meeting
display_title: Join a Meeting
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting)

Joining a meeting using the Webex Meetings Web SDK allows you to participate in video conferences. This article guides you through the process of joining a meeting and covers various additional scenarios, including joining with or without media, configuring audio and video settings, and screen sharing.

## The Meeting Instance

A Meeting instance represents a specific meeting session within the Webex Meetings SDK. Each meeting has its Meeting instance, which allows you to interact with and control the meeting's behavior.

## Fetch a Meeting Instance

A `meeting` instance is typically created once a meeting is initiated through the SDK. If a meeting has already been created on the SDK, you can retrieve it using the SDK's `meetings` object by passing a `meetingId`.



> **Info**
>
> This method does not fetch the list of all meetings from the Webex cloud. It only lists the meetings that are created either with `webex.meetings.create` or `webex.meetings.syncMeetings`.



```js
const meeting = webex.meetings.getAllMeetings()[meetingId];
```

If participants have already joined the meeting, it can be retrieved from Webex Cloud. Refer to [Sync Meetings](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction#synchronize-meetings-from-webex-cloud).

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

### Join a Meeting Without Media

A participant can join without any media connection initially and can set up media options later as required.

To join a meeting without media:

```js
meeting.join().then(() => {
  // Meeting joined successfully
});
```

### Add Media to a Meeting

To join with a meeting with media enabled, you must create media streams first, before adding the media to the meeting.

#### Set up Media Streams

To create various `MediaStreams` object streams like microphone, video, and screen sharing:

```js
const audioVideoConstraints = {
  audio: { deviceId: audioDeviceId },
  video: { deviceId: videoDeviceId }
};

const microphoneStream =
  await webex.meetings.mediaHelpers.createMicrophoneStream(constraints.audio);
const cameraStream = await webex.meetings.mediaHelpers.createCameraStream(
  constraints.video
);
const [localShareVideoStream, localShareAudioStream] =
  await webex.meetings.mediaHelpers.createDisplayStreamWithAudio();
```

For more info on the `MediaStreams` object, see [Media Streams Management](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects).

#### The addMedia() method

Once a participant has joined the meeting, the participant's media streams can be added using the `addMedia()` method. Media streams can be of different types: `LocalMicrophoneStream` for audio, `LocalCameraStream` for video, and `MediaStream` that encapsulates audio or video. 

#### Use addMedia() with LocalMicrophoneStream and LocalCameraStream

When we create a media stream object using `createMicrophoneStream()` and `createCameraStream()`, it returns a media stream of type `LocalMicrophoneStream` for audio and `LocalCameraStream` for video. This type of media stream can be passed in `addMedia()` :

```js
const addMediaOptions = {
  localStreams: {
    microphone: microphoneStream,
    camera: cameraStream,
  },
  allowMediaInLobby: true,
};

await meeting.addMedia(addMediaOptions);
```

#### Use addMedia() with MediaStream

If the media stream is of type `MediaStream`, it needs to be typecast as `LocalMicrophoneStream` for audio and `LocalCameraStream` for video before passing it to the `addMedia()` method:

```js
const microphoneStream = new LocalMicrophoneStream(mediaStream);
const camerStream = new LocalCameraStream(mediaStream)

const addMediaOptions = {
  localStreams: {
    microphone: microphoneStream,
    camera: cameraStream,
  },
  allowMediaInLobby: true,
};

await meeting.addMedia(addMediaOptions);
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
        <strong>Parameters (AddMediaOptions)</strong>
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
                  Local audio and video Stream objects
                </td>
                <td><strong>LocalStreams</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>audioEnabled</code></td>
                <td>
                  Allow or block audio while in the meeting
                </td>
                <td><strong>Boolean</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>videoEnabled</code></td>
                <td>
                  Allow or block video while in the meeting
                </td>
                <td><strong>Boolean</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>shareAudioEnabled</code></td>
                <td>
                  Allow or block audio while sharing in the meeting
                </td>
                <td><strong>Boolean</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>shareVideoEnabled</code></td>
                <td>
                  Allow or block sharing in the meeting
                </td>
                <td><strong>Boolean</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>remoteMediaManagerConfig</code></td>
                <td>
                  Remote Media Manager configuration. Refer to the Multistream comprehensive guide for more information. Only applicable in multistream meetings.
                </td>
                <td><strong>RemoteMediaManagerConfiguration</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>allowMediaInLobby</code></td>
                <td>
                  Allow or block media while in the lobby of the meeting
                </td>
                <td><strong>Boolean</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td><code>additionalMediaOptions</code></td>
                <td>
                  Granular controls over the media in the meeting. These options allow you to set whether you'd like to only send or receive audio or video. These controls require the audioEnabled and videoEnabled flags to be set to true. Only applicable for transcoded meetings.
                </td>
                <td><strong>Object</strong></td>
                <td>No</td>
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

To add media, configure the streams using the `localStreams` attribute in the `addMediaOptions` object.

#### The LocalStreams object

The `LocalStreams` object is a collection of different `LocalStream` objects that define the media within a meeting context.

The `LocalStream` serves as a common interface implemented by various classes, each representing different types of media streams. The classes, which include `LocalMicrophoneStream`, `LocalCameraStream`, `LocalSystemAudioStream`, and `LocalDisplayStream`, implement the `LocalStream` interface to provide specific functionality for managing various media streams.

The `LocalStreams` contains the following attributes:



| **Name**              | **Type**                   | **Optional** |
| ----------------- | ---------------------- | -------- |
| `microphone`        | **LocalMicrophoneStream**  | Yes      |
| `camera`            | **LocalCameraStream**      | Yes      |
| `screenShare.audio` | **LocalSystemAudioStream** | Yes      |
| `screenShare.video` | **LocalDisplayStream**     | Yes      |



> **Info**
>
> The audio feature for screen sharing doesn't work in a single stream, so switching to multistream is advisable. It's also important to note that even in multistream, screen share audio is only supported when you share a browser tab, not when sharing a window or the entire screen, due to browser limitations.



### Join a Meeting with Media

To join a meeting with media enabled, define a `joinOptions` object and pass it to the `Meeting` object's `join()` method:

```js
const joinOptions = {
  enableMultistream: false, // Multistream is an experimental feature
  pin: 'pin',
  moderator: false,
  breakoutsSupported: false, // Enable breakout rooms in the meeting
};

await meeting.join(joinOptions);
```

See above for information on the `joinOptions` object.

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
