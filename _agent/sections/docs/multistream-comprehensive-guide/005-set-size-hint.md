---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Set Size Hint
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

## Set Size Hint

Clients can specify a size hint if they are displaying remote video on screens of varying sizes and need to adjust the video resolution for optimal display or bandwidth conservation. When the remote receives this hint, it starts transmitting the video at the requested resolution.

`setSizeHint()` can be invoked on the `remoteMedia` object. Each video stream corresponds to a `remoteMedia` object.

```js
remoteMedia.setSizeHint(width, height);
```

**Asynchronous**: No

**Parameters**:



| **Name** | **Description**              | **Type** | **Mandatory** |
| -------- | ---------------------------- | -------- | ------------- |
| `width`  | Width of the video element.  | number   | Yes           |
| `height` | Height of the video element. | number   | Yes           |

**Returns** - void
