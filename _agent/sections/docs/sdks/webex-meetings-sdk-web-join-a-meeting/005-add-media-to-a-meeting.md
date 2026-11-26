---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-join-a-meeting
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Join a Meeting
- Add Media to a Meeting
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
