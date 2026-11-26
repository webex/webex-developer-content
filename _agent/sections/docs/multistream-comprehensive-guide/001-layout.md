---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Layout
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

## Layout

A "layout" refers to the arrangement of remote streams in the user interface. Multistream allows you to customize this layout. To do so, call `addMedia()` with the desired layout details. The existing arguments for `addMedia()` are unaffected by this process. For more information, refer to [this documentation](https://github.com/webex/webex-js-sdk/wiki/Joining-a-Meeting#the-addmedia-method).

The `AddMediaOptions` now includes a new property, `remoteMediaManagerConfig`, for multistream functionality. To implement a custom layout, you can use the same data format as shown in the predefined layouts.

The following are the default configuration values for `remoteMediaManagerConfig`, which are used if no overrides are provided:

```js
const remoteMediaManagerConfig = {
  audio: {
    numOfActiveSpeakerStreams: 3,
    numOfScreenShareStreams: 1,
  },
  video: {
    preferLiveVideo: true,
    initialLayoutId: 'AllEqual',

    layouts: {
      AllEqual: AllEqualLayout,
      OnePlusFive: OnePlusFiveLayout,
      Single: SingleLayout,
      Stage: Stage2x2With6ThumbnailsLayout,
      ScreenShareView: RemoteScreenShareWithSmallThumbnailsLayout,
    }
  }
}
```

A detailed explanation of this object can be found [here](https://developer.webex.com/docs/multistream-comprehensive-guide#remotemediamanager-configuration-object).

Here are the predefined layouts for the default configuration:



| **Type**        | **Description**               |
| --------------- | ----------------------------- |
| `AllEqual`        | All equal (max 9).            |
| `OnePlusFive`     | One big pane + five small.    |
| `Single`          | Single Video pane.            |
| `Stage`           | Stage with thumbnails.        |
| `ScreenShareView` | Screen share with thumbnails. |

### Layout Details

The following setions describe each available layout in detail.

#### AllEqual

An "all equal" grid, with size up to 3 x 3 = 9.

![All equal grid](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt93ced44d5f0199da/AllEqual.jpg)

**Example**

```js
const AllEqualLayout: VideoLayout = {
  activeSpeakerVideoPaneGroups: [
    {
      id: 'main',
      numPanes: 9,
      size: 'best',
      priority: 255,
    },
  ],
};
```

#### OnePlusFive

A layout with one big pane for the highest-priority active speaker and 5 small panes for other active speakers.

![One plus 5 layout](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7e724cd044eba1dd/OnePlusFive.jpg)

**Example**

```js
const OnePlusFiveLayout: VideoLayout = {
  activeSpeakerVideoPaneGroups: [
    {
      id: 'mainBigOne',
      numPanes: 1,
      size: 'large',
      priority: 255,
    },
    {
      id: 'secondarySetOfSmallPanes',
      numPanes: 5,
      size: 'very small',
      priority: 254,
    },
  ],
};
```

#### Single

A layout with a single remote active speaker video pane.

![Single remote speaker video pane](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltca4fb1beb9e74f00/Single.jpg)

**Example**

```js
const SingleLayout: VideoLayout = {
  activeSpeakerVideoPaneGroups: [
    {
      id: 'main',
      numPanes: 1,
      size: 'best',
      priority: 255,
    },
  ],
};
```

#### Stage

A staged layout with four pre-selected meeting participants in the main 2x2 grid and 6 small panes for other active speakers at the top.

The predetermined participants can be included using the [CSI](https://developer.webex.com/docs/multistream-comprehensive-guide#get-an-array-of-a-members-csis) value, which can be [updated](https://developer.webex.com/docs/multistream-comprehensive-guide#set-remote-video-csi) once the values are accessible after joining the meeting.

![Staged layout](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3cbf1e3a49fd8255/Stage.jpg)

**Example**

```js
const Stage2x2With6ThumbnailsLayout: VideoLayout = {
  activeSpeakerVideoPaneGroups: [
    {
      id: 'thumbnails',
      numPanes: 6,
      size: 'thumbnail',
      priority: 255,
    },
  ],
  memberVideoPanes: [
    {id: 'stage-1', size: 'medium', csi: undefined},
    {id: 'stage-2', size: 'medium', csi: undefined},
    {id: 'stage-3', size: 'medium', csi: undefined},
    {id: 'stage-4', size: 'medium', csi: undefined},
  ],
};
```

#### ScreenShareView

A strip of eight small video panes (thumbnails) displayed at the top of a remote screenshare.

![Eight small video panes](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt77752ce65dbc306e/Screenshare.jpg)

**Example**

```js
const RemoteScreenShareWithSmallThumbnailsLayout: VideoLayout = {
  screenShareVideo: {size: 'best'},
  activeSpeakerVideoPaneGroups: [
    {
      id: 'thumbnails',
      numPanes: 8,
      size: 'thumbnail',
      priority: 255,
    },
  ],
};
```

### RemoteMediaManager Configuration Object

This object configures the `RemoteMediaManager`. Based on this configuration, you will receive the multistream remote media.

```js
{
  audio: {
    numOfActiveSpeakerStreams: number; 
    numOfScreenShareStreams: number; 
  };
  video: {
    preferLiveVideo: boolean; 
    initialLayoutId: LayoutId;

    layouts: {[key: LayoutId]: VideoLayout}; 
  };
}
```

#### Properties of the Audio Object



| **Name**                    | **Description**                                                                                                    | **Type** |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------ | -------- |
| `numOfActiveSpeakerStreams` | The maximum number of speakers that can be heard simultaneously.                                                   | Number   |
| `numOfScreenShareStreams`   | The maximum number of screenshare streams. Typically, one should suffice as only one person can present at a time in Webex. | Number   |

#### Properties of Video Object



| **Name**          | **Description**                                                                                                                      | **Type** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| `preferLiveVideo` | If set to true, the server prioritizes sending streams of participants with their video enabled over those that don't send video. | boolean  |
| `initialLayoutId` | One of the keys defined within the layouts object.                                                                                   | string   |
| `layouts`         | Key-value pairs where the value determines the layout. Additional details are provided in the following table.                          | object   |

#### Properties of VideoLayout Object



| **Name**                       | **Description**                   | **Type**                         |
| ------------------------------ | --------------------------------- | -------------------------------- |
| `screenShareVideo`             | Defines the screenshare stream.   | `{ size: PaneSize }`             |
| `activeSpeakerVideoPaneGroups` | Defines the active speaker panes. | `Array<ActiveSpeakerPaneObject>` |
| `memberVideoPanes`             | Defines the member video panes.   | `Array<MemberPaneObject>`        |

#### Values for the PaneSize Object



| **PaneSize** | **Description**                                |
| ------------ | ---------------------------------------------- |
| `thumbnail`  | The smallest possible resolution, 90p or less. |
| `very small` | 180p or less.                                  |
| `small`      | 360p or less.                                  |
| `medium`     | 720p or less.                                  |
| `large`      | 1080p or less.                                 |
| `best`       | Highest possible resolution.                   |

#### Properties of ActiveSpeakerPaneObject



| **Name**   | **Description**                                                                   | **Type**          |
| ---------- | --------------------------------------------------------------------------------- | ----------------- |
| `id`       | An arbitrary value.                                                               | string            |
| `numPanes` | The number of streams that you will receive.                                      | number            |
| `size`     | The size of each stream.                                                          | `PaneSize` (string) |
| `priority` | The priority of the streams. The most recent active speaker has the highest priority. | number (0-255)    |



> **Info**
>
> Consider the following scenario with two groups:
> - Group A: Priority 255, contains 1 video pane
> - Group B: Priority 254, contains 5 video panes
> In a meeting with 6 attendees, when person X begins speaking, they appear in Group A. If person Z starts speaking next, Z will be displayed in Group A, and X will move to Group B.



#### Properties of MemberPaneObject



| **Name** | **Description**                                                                                                 | **Type**          |
| -------- | --------------------------------------------------------------------------------------------------------------- | ----------------- |
| `id`     | An arbitrary value (e.g., `stage-1`).                                                                           | string            |
| `size`   | The size of the stream.                                                                                         | `PaneSize` (string) |
| `csi`    | A unique identifier for a stream. When a client generates a stream, it assigns a CSI value to it.               | number            |

Member video panes can only be accessed within the stage layout, which allows for the pinning of specific participants' positions in the layout. The stage layout is created when memberVideoPanes is included in the layout configuration. In this case, developers are responsible for managing and displaying participants as they join or leave. This is different from activeSpeakerVideoPaneGroups, where a consistent list of streams featuring active speakers/participants is always received. Additionally, the active speaker video pane can be pinned. Therefore, participants can be pinned either by using memberVideoPanes or by invoking pinActiveSpeakerVideoPane(remoteMedia, csi) for activeSpeakerVideoPaneGroups.

Each member or participant can have multiple streams. These streams can be of various types such as audio, video, screenshareVideo, or screenshareAudio. Each stream is uniquely identified by a CSI. A member can have more than one stream of the same type. For instance, a user can have two video streams (each with a unique CSI) if they join the meeting using multiple devices.

In most scenarios, you'll primarily utilize `activeSpeakerVideoPaneGroups`.
