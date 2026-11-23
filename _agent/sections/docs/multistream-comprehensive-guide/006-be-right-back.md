---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Be Right Back
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

## Be Right Back

The `meeting.beRightBack()` allows the update of the "be right back" status for the current participant.

It can be used when a participant would like to step away from a meeting for a short period of time.
When enabled, the participant's video stream could be replaced with a placeholder image, etc.

This method is applicable only to multistream meetings. 
It will throw an error if attempted in a non-multistream meeting.

```js
await meeting.beRightBack(true);
```

**Asynchronous**: Yes

**Parameters**:



| **Name** | **Description**               | **Type** | **Mandatory** |
| -------- |-------------------------------| -------- | ------------- |
| `enabled` | Whether or not be right back should be enabled. | boolean  | Yes           |

**Returns**: `Promise<void>`
