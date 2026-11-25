---
type: Excerpt
canonical_url: https://developer.webex.com/docs/multistream-comprehensive-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Methods
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

## Methods

Multiple methods are available for handling various scenarios and updating the layout.

### Get an Array of a Member's CSIs

```js
const csiList = meeting.members.getCsisForMember(memberId, mediaType='video', mediaContent='main');
```

**Asynchronous**: No

**Parameters**



| **Name**       | **Description**                 | **Type**                   | **Mandatory** |
| -------------- | ------------------------------- | -------------------------- | ------------- |
| `memberId`     | Member's ID.                    | string                     | Yes           |
| `mediaType`    | The media type.                 | `audio`, `video` (Default) | No            |
| `mediaContent` | Type of media content.          | `main` (Default), `slides` | No            |

**Returns**: `Array<number>`

### Find A Member by CSI

```js
const member = meeting.members.findMemberByCsi(csi);
```

**Asynchronous**: No

**Parameters**:



| **Name** | **Description**                  | **Type** | **Mandatory** |
| -------- | -------------------------------- | -------- | ------------- |
| `csi`    | CSI number linked to the stream. | number   | Yes           |

**Returns**: Member
