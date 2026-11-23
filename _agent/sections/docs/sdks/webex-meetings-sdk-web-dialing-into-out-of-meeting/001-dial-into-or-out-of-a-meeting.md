---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-dialing-into-out-of-meeting
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Dial Into or Out of a Meeting
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

## Dial Into or Out of a Meeting

A user can trigger the dial-in or dial-out using the `Meeting` object's [usePhoneAudio](https://webex.github.io/webex-js-sdk/api/#meetingusephoneaudio) method and passing an optional phone number as a String:

```js
await meeting.usePhoneAudio(phoneNumber);
```



|  |  |
| --- | --- |
| **Asynchronous** | Yes |
| **Parameters** | **String** - `phoneNumber` (Optional) |
| **Returns** | `Promise` Resolves once the dial-in or dial-out request gets completed, or rejects if it fails |

When a phone number is provided, the SDK provisions a device for dial out functionality, and initiates a call to the specified phone number. When a user answers the call, the meeting's audio input and output are connected to the phone device. In the absence of a phone number, the SDK defaults to provisioning a device for the dial in functionality.

The SDK is designed to provision only one device each for either dialing in or out. Once a device is provisioned, subsequent calls to the `usePhoneAudio()` method do not result in additional provisioning.
