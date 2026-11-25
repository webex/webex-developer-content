---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Stream Mute Options
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-migrating-2-to-3). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-migrating-2-to-3.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article outlines the migration process for developers who are moving their Webex Web SDK applications from version 2 to version 3. It provides information on the most important changes to the SDK to aid our existing developers in making their applications compatible with SDK version 3.

## Selected section

## Stream Mute Options

To accommodate the distinction between muting devices programmatically and muting them via a physical button, modifications have been made to the APIs associated with LocalStream and RemoteStream. Some devices, such as Chromebooks, have a physical button that allows users to mute and unmute their microphone or camera. When a device is muted using this physical button, it cannot be unmuted programmatically; the user must manually press the button again to unmute it.

The API changes ensure that developers can identify the mute state accurately and respond appropriately within their applications, regardless of whether the mute action was initiated by software or hardware.



> **Info**
>
> This breaking change is part of version `webex@3.0.0-next.10` and later.



### LocalTrack's `setMuted` method
#### 2.x

This is the method that is to be used to programmatically mute a `LocalTrack` in the V2 SDK.

```javascript
localTrack.setMuted(true); // Set to false in order to unmute.
```

#### 3.x

In the V3 SDK, this method is renamed as follows:

```javascript
localStream.setUserMuted(true); // Set to false in order to unmute.
```

### LocalTrack's `mute-state-change` event
#### 2.x

This event is triggered when the mute state of a local track changes programmatically.

```javascript
localTrack.on('mute-state-change', (isMuted) => {
  // Update the UI to reflect the mute state change.
});
```

#### 3.x
The `mute-state-change` event is replaced and split into two:

**`user-mute-state-change`**
This is the event that's fired when the mute state changes programmatically.

```javascript
localStream.on('user-mute-state-change', (isUserMuted) => {
  // This handler is triggered when the user toggles the mute programmatically.
  // 'isUserMuted' indicates the new mute state: true for muted, false for unmuted.
});
```

**`system-mute-state-change`**
This is the event that's fired when the mute state changes through a physical button.

```javascript
localStream.on('system-mute-state-change', (isSystemMuted) => {
  // Triggered when the user mutes through a physical button.
  // At this point, it is important to note that the unmute button won't work if 'isSystemMuted' is true.
  // You can use this to disable the unmute button and add a UI note stating that the user has to unmute their hardware.
});
```

### LocalTrack's `muted` getter
This remains unchanged. It will return true in either case (programmatically muted or hardware muted).

#### 3.x

However, in 3.x, two new getters are introduced:
- `LocalStream.userMuted` - true when programmatically muted
- `LocalStream.systemMuted` - true when muted via hardware

### RemoteTrack's `muted` getter

#### 2.x
This getter is used to identify if a remote track is muted or not.

```javascript
const isRemoteMuted = remoteTrack.muted;
```

#### 3.x
The `muted` is replaced by the `mediaState` getter which can be used as follows,

```javascript
const isRemoteMuted = remoteStream.mediaState !== 'started';
```

Basically, the getter `remoteStream.mediaState` will return either `started` or `stopped`, meaning the stream is not muted or muted, respectively.

### RemoteTrack's `mute-state-change` event

#### 2.x

This event is subscribed to in order to know if the remote track's mute state changes.

```javascript
remoteTrack.on('mute-state-change', (isMuted) => {
  // Implement functionality to handle mute state change.
  // 'isMuted' indicates whether the remote track is muted or not.
});
```

#### 3.x

The existing `mute-state-change` event is replaced with the `media-state-change` event, and it can be used as follows:

```javascript
remoteStream.on('media-state-change', (mediaState) => {
  // 'mediaState' can be either 'started' or 'stopped'.
  // 'started' indicates the media is unmuted.
  // 'stopped' indicates the media is muted.
  
  // Implement the logic based on the media state.
  if (mediaState === 'started') {
    // Handle the unmuted state.
  } else if (mediaState === 'stopped') {
    // Handle the muted state.
  }
});
```
