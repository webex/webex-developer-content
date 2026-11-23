---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Disconnect Dial In or Out Calls
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

When connected to a meeting, the following dialing capabilities are available:

- **Dial out**: Allows the system to call a user's phone, enabling it to be used as the audio input/output device for the meeting.
- **Dial in**: Permits users to call into Webex and use their phone as the meeting's audio input/output device.

<br/>

The SDK also provides functionality to remotely end phone calls in both of the above scenarios.

## Selected section

## Disconnect Dial In or Out Calls

Disconnect dial-in or dial-out calls using the `Meeting` object's [disconnectPhoneAudio](https://webex.github.io/webex-js-sdk/api/#meetingdisconnectphoneaudio) method:

```js
await meeting.disconnectPhoneAudio();
```



|  |  |
| --- | --- |
| **Asynchronous** | Yes |
| **Parameters** | None |
| **Returns** | `Promise` Resolves once the phone audio disconnection has been completed. |
