---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Remote Media Manager
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

## Remote Media Manager

In multistream meetings, the `meeting.addMedia()` API establishes the media connection. It configures streams to receive remote media based on the `remoteMediaManagerConfig` provided as an option.

The `Meeting.addMedia()` method accepts an optional configuration object to set up the `RemoteMediaManager`:

```js
meeting.addMedia({
  ...,
  remoteMediaManagerConfig?: RemoteMediaManagerConfiguration;
})
```

**RemoteMediaManager configuration object**

```js
{
  audio: {
    numOfActiveSpeakerStreams: number; // number of audio streams we want to receive
    numOfScreenShareStreams: number; // 1 should be enough because in Webex only 1 person at a time can be presenting screen share
  };
  video: {
    preferLiveVideo: boolean; // applies to all pane groups with active speaker policy
    initialLayoutId: LayoutId;

    layouts: {[key: LayoutId]: VideoLayout}; // a map of all available layouts, a layout can be set via setLayout() method
  };
}
```

This object's details are outlined in the [Explanation of the RemoteMediaManager Object](https://developer.webex.com/docs/multistream-comprehensive-guide#remotemediamanager-configuration-object) section.

### Set a Remote Video CSI

```js
meeting.remoteMediaManager.setRemoteVideoCsi(remoteMedia, csi);
```

**Asynchronous**: No

**Parameters**:



| **Name**      | **Description**                                                  | **Type**     | **Mandatory** |
| ------------- | ---------------------------------------------------------------- | ------------ | ------------- |
| `remoteMedia` | `RemoteMedia` object.                                              | RemoteMedia  | Yes           |
| `csi`         | A new CSI value, can be null if we want to stop receiving media. | number, null | Yes           |

**Returns**: void

### Add a Member Video Pane

```js
const remoteMedia = await meeting.remoteMediaManager.addMemberVideoPane(
  { id: PaneId; size: PaneSize; csi?: CSI; }
);
```

**Asynchronous**: Yes

**Parameters**:



| **Name** | **Description**                        | **Type**                                                      | **Mandatory** |
| -------- | -------------------------------------- | ------------------------------------------------------------- | ------------- |
| `id`     | Pane ID.                               | string                                                        | Yes           |
| `size`   | Size of the video pane.                | `thumbnail`, `very small`, `small`, `medium`, `large`, `best` | Yes           |
| `csi`    | CSI number associated with the stream. | number                                                        | No            |

**Returns**: `Promise<RemoteMedia>`

### Get the Currently Selected Layout ID

```js
const layoutId = meeting.remoteMediaManager?.getLayoutId();
```

**Asynchronous**: No

**Parameters**: No

**Returns**: string

### Change the Layout

Calling this method triggers the `media:remoteVideo:layoutChanged` event.

```js
await meeting.remoteMediaManager.setLayout(layoutId);
```

**Asynchronous**: Yes

**Parameters**:



| **Name**   | **Description**           | **Type** | **Mandatory** |
| ---------- | ------------------------- | -------- | ------------- |
| `layoutId` | ID of the defined layout. | string   | Yes           |

**Returns**: `Promise<void>`

### Set the prefer live video

```js
meeting.remoteMediaManager.setPreferLiveVideo(preferLiveVideo);
```

**Asynchronous**: No

**Parameters**:



| **Name**          | **Description**                                                           | **Type** | **Mandatory** |
| ----------------- | ------------------------------------------------------------------------- | -------- | ------------- |
| `preferLiveVideo` | If enabled, this option will prioritize retrieving streams with active video. | boolean  | Yes           |

**Returns** - void

### Set Active Speaker CSIs

Set CSIs for multiple `RemoteMedia` instances belonging to a `RemoteMediaGroup`.

```js
meeting.remoteMediaManager.setActiveSpeakerCsis(remoteMediaCsis);
```

**Asynchronous**: No

**Parameters**: An array of object with the following properties, for example, `Array<{ remoteMedia, csi }>`.



| **Name**      | **Description**                        | **Type**    | **Mandatory** |
| ------------- | -------------------------------------- | ----------- | ------------- |
| `remoteMedia` | The remote media object.               | RemoteMedia | Yes           |
| `csi`         | CSI number associated with the stream. | number      | No            |

**Returns**: void



> **Info**
>
> For each entry in the `remoteMediaCsis` array:
> - If `csi` is specified, the `RemoteMedia` instance is pinned to that CSI.
> - If `csi` is undefined, the `RemoteMedia` instance gets unpinned.



### Set a Remote Video CSI

Set a new CSI on a given remote media object

```js
meeting.remoteMediaManager.setRemoteVideoCsi(remoteMedia, csi);
```

**Asynchronous**: No

**Parameters**:



| **Name**      | **Description**                                                      | **Type**         | **Mandatory** |
| ------------- | -------------------------------------------------------------------- | ---------------- | ------------- |
| `remoteMedia` | The remote media object to be altered.                               | RemoteMedia      | Yes           |
| `csi`         | A new CSI value. It can be null if you wish to stop receiving media. | `number`, `null` | Yes           |

**Returns** - void

### Add a Member Video Pane

Add a new member video pane to the currently selected layout.

```js
const remoteMedia = await meeting.remoteMediaManager.addMemberVideoPane(newPane);
```

**Asynchronous**: Yes

**Parameters**:



| **Name** | **Description** | **Type**                                                      | **Mandatory** |
| -------- | --------------- | ------------------------------------------------------------- | ------------- |
| `id`     | Pane ID.        | string                                                        | Yes           |
| `size`   | Pane size.      | `thumbnail`, `very small`, `small`, `medium`, `large`, `best` | Yes           |
| `csi`    | New CSI value.  | number                                                        | No            |

**Returns** - `Promise<RemoteMedia>`



> **Info**
>
> Changes to the layout are lost after a layout change.



### Remove Member Video Pane

Remove a member video pane from the currently selected layout.

```js
await meeting.remoteMediaManager.removeMemberVideoPane(paneId);
```

**Asynchronous**: Yes

**Parameters**:



| **Name** | **Description** | **Type** | **Mandatory** |
| -------- | --------------- | -------- | ------------- |
| `paneId` | Pane ID.        | string   | Yes           |

**Returns** - `Promise<void>`



> **Info**
>
> Changes to the layout are lost after a layout change.



### Pin an Active Speaker Video Pane

Pin an active speaker remote media object to the given CSI value.

```js
meeting.remoteMediaManager.pinActiveSpeakerVideoPane(remoteMedia, csi);
```

This function pins an active speaker's remote media object to a specified CSI value. Consequently, the remote media will only play audio/video from that specific CSI. This remains in effect until either the `unpinActiveSpeakerVideoPane()` function is called or the current layout is altered.

**Asynchronous**: No

**Parameters**:



| **Name**      | **Description**                                                      | **Type**    | **Mandatory** |
| ------------- | -------------------------------------------------------------------- | ----------- | ------------- |
| `remoteMedia` | Reference to the remote media object.                                | `RemoteMedia` | Yes           |
| `csi`         | CSI value to pin to. If undefined, the current CSI value is used.    | number      | No            |

**Returns** - void

### Unpin Active Speaker Video Pane

Unpin a remote media object from the specific CSI value to which it was previously pinned.

```js
meeting.remoteMediaManager.unpinActiveSpeakerVideoPane(remoteMedia);
```

**Asynchronous**: No

**Parameters**:



| **Name**      | **Description**                | **Type**    | **Mandatory** |
| ------------- | ------------------------------ | ----------- | ------------- |
| `remoteMedia` | Remote media object reference. | `RemoteMedia` | Yes           |

**Returns** - void

### Pinned

Determine whether a given remote media object is part of an active speaker group and if it has been pinned.

```js
const isPinned = meeting.remoteMediaManager.isPinned(remoteMedia);
```

**Asynchronous**: No

**Parameters**:



| **Name**      | **Description**                | **Type**    | **Mandatory** |
| ------------- | ------------------------------ | ----------- | ------------- |
| `remoteMedia` | Remote media object reference. | `RemoteMedia` | Yes           |

**Returns** - boolean



> **Info**
>
> Throws an error if the remote media object doesn't belong to any active speaker remote media group.
