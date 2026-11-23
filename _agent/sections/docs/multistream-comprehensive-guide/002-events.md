---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Events
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/multistream-comprehensive-guide). [Full Markdown](../../../../docs/multistream-comprehensive-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Developers have a variety of options to customize how they choose to display remote videos with multistream media.

---

The initial step in utilizing Multistream is to include **enableMultistream** within the **joinOptions** parameter for both the `meeting.join()` and `meeting.joinWithMedia()` methods. 

**Example**

```js
const joinOptions = {
  enableMultistream: true,
  ...
};

await meeting.join(joinOptions);

// or

await meeting.joinWithMedia({joinOptions, mediaOptions});
```

This article is divided into three sections:

1. **Layouts**: Determines the preferred visualization of the remote streams.
2. **Events**: Monitors all remote streams and additional events.
3. **Methods** and **RemoteMediaManager**: Facilitates layout updates and other operations.

**Terminology**

Throughout this document we'll refer to the following terms:

- **Layout**: An arrangement of remote streams in the user interface.
- **Pane**: An individual element within the layout grid.
- **Remote Media**: The media stream and associated details.
- **Remote Media Group**: A collection of remote media as a group, along with additional helper APIs.
- **CSI**: A unique identifier linked to a stream, connecting a member participant with that stream.

## Selected section

## Events

Events can be listened to using the `meeting.on()` method.

Here's an example:

```js
meeting.on('event name', (data) => {
  console.log(data);
});
```



> **Info**
>
> When multistream is enabled, media cannot be accessed or listened to on the `media:ready` event. Instead, you should listen to the media events received during a meeting that pertain to multistream, such as the events mentioned below, to handle media streams appropriately.



```js
meeting.on('media:remoteVideo:layoutChanged', ({
  layoutId, activeSpeakerVideoPanes, memberVideoPanes, screenShareVideo
}) => {
  console.log('layoutId: ', layoutId);
  console.log('activeSpeakerVideoPanes:', activeSpeakerVideoPanes);
  console.log('memberVideoPanes:', memberVideoPanes);
  console.log('screenShareVideo:', screenShareVideo);
});
```



> **Info**
>
> The event `media:remoteVideo:layoutChanged` will be triggered with the `initialLayoutId` the first time, even if there are no changes in the layout.



### Media Events

The following table and sections elaborate on the media events received during a meeting that pertain to multistream.



| **Event name**                         | **Data Received**                                                                 |
| -------------------------------------- | --------------------------------------------------------------------------------- |
| `media:remoteAudio:created`            | List of audio streams (remains unchanged by layout changes).                      |
| `media:remoteScreenShareAudio:created` | Object representing the screen share audio media group.                           |
| `media:remoteVideo:layoutChanged`      | `{ layoutId, activeSpeakerVideoPanes, memberVideoPanes, screenShareVideo }`.      |
| `media:remoteVideoSourceCountChanged`  | Number of remote video sources (`{ numTotalSource, numLiveSources }`).            |
| `media:remoteAudioSourceCountChanged`  | Number of remote audio sources (`{ numTotalSource, numLiveSources }`).            |
| `media:activeSpeakerChanged`           | List of member IDs for active speakers (`{ memberIds }`).                         |



> **Info**
>
> The list of audio streams received in the `media:remoteAudio:created` event does not contain participant ID information. It is also not possible to correlate a single audio stream with the participant that is speaking.



#### media:remoteScreenShareAudio:created

To obtain the list of remote media elements from the group, invoke `getRemoteMedia()`.

```js
const remoteMedia = screenShareAudioMediaGroup.getRemoteMedia()[0];
const remoteMediaStream = remoteMedia.stream;
```

**Asynchronous**: No

**Parameters**



| **Name** | **Description**                                                   | **Type**                              | **Mandatory** |
| -------- | ----------------------------------------------------------------- | ------------------------------------- | ------------- |
| `filter` | A string used to filter and retrieve a specific type of remote media. | `all` (Default), `pinned`, `unpinned` | No            |

**Returns**: `Array<RemoteMedia>`

#### media:remoteVideo:layoutChanged



| **Data Received**         | **Description**                                                                 |
| ------------------------- | ------------------------------------------------------------------------------- |
| `layoutId`                | Options: `AllEqual`, `OnePlusFive`, `Single`, `Stage`, `ScreenShareView`        |
| `activeSpeakerVideoPanes` | Contains: `groupId`, `groupRemoteMedia`                                        |
| `memberVideoPanes`        | Contains: `paneId`, `remoteMedia`                                              |
| `screenShareVideo`        | RemoteMedia object: `{ id, stream, sourceState (either 'no source' or 'live'), memberId }` |



> **Info**
>
> The `layoutId` list displayed here corresponds to those defined in the configuration. These IDs may vary depending on your configuration settings.



#### media:remoteVideoSourceCountChanged



| **Data Received** | **Description**                          |
| ----------------- | ---------------------------------------- |
| `numTotalSource`  | Total number of all video sources.       |
| `numLiveSources`  | Total number of live video sources.      |

#### media:remoteAudioSourceCountChanged



| **Data Received** | **Description**                          |
| ----------------- | ---------------------------------------- |
| `numTotalSource`  | Total number of all audio sources.       |
| `numLiveSources`  | Total number of live audio sources.      |

### Meeting Events

The following table and sections elaborate on the meeting events received during a meeting that pertain to multistream.



| **Event name**                    | **Description**                                                                                                                                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `meeting:stoppedSharingLocal`     | The client has stopped screen sharing and no longer has control over it. This can occur when another participant starts sharing and takes control, or if the user stops sharing.                                 |
| `meeting:startedSharingRemote`    | Another participant in the meeting has started screen sharing and now has control over it.                                                                                                                      |
| `meeting:stoppedSharingRemote`    | Another participant in the meeting has stopped screen sharing and no longer has control over it.                                                                                                                |

### Remote Media Events

The `remoteMedia` object may include streams from various participants and can dynamically update as different participants begin speaking. The `memberId` within the `remoteMedia` object allows for the display of corresponding names or data alongside the stream. This `memberId` can be utilized to retrieve the name of the participant.

Events can be listened to using the `remoteMedia.on()` method.

**Example**

```js
remoteMedia.on('Event name', (data) => {
  console.log(data);
});
```



| **Event name** | **Description**                                                                 |
| -------------- | ------------------------------------------------------------------------------- |
| `sourceUpdate` | Triggered when the source of the `remoteMedia` changes, such as when another participant begins speaking. |
| `stopped`      | Triggered when the participant has deactivated their stream.                    |

With `sourceUpdate`, you can inspect the `memberId` and `sourceState` to obtain the most recent information about the `remoteMedia`.

Here's the possible information received during the `sourceUpdate` event:



| **Data Received**    | **Description**                                                   |
| -------------------- | ----------------------------------------------------------------- |
| `no source`          | No video is available.                                            |
| `invalid source`     | The source is invalid.                                            |
| `live`               | The video is available.                                           |
| `avatar`             | The camera is muted or there is no video. An avatar can be shown. |
| `bandwidth disabled` | There is insufficient bandwidth to show the video. An avatar can be shown. |
| `policy violation`   | Video is restricted due to a policy violation.                    |
