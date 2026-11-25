---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Agent Login
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-authentication.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This guide covers authentication; session registration and cleanup; agent station login and logout; automatic relogin; multi-login behavior; and agent state management in the Contact Center SDK.

---



> **Info**
>
> Note: For single-session apps, you can rely on method promises alone, subscribe to events mainly for multi-session support (for example, handling more than one active session).

<br>

## Selected section

## Agent Login

Use `stationLogin` to log the agent into a specific device type:

```javascript
await webex.cc.stationLogin({
  teamId: '<TEAM_ID>',
  loginOption: 'BROWSER' | 'EXTENSION' | 'AGENT_DN',
  dialNumber: '<DN-OR-EXT>' // required for EXTENSION and AGENT_DN; ignored for BROWSER
});
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `teamId` | string | yes | Team id to log the agent into. Typically taken from the profile returned by `register()`. |
| `loginOption` | string | yes | Device type to use. One of `BROWSER`, `EXTENSION`, `AGENT_DN`. |
| `dialNumber` | string | conditional | Required for `EXTENSION` and `AGENT_DN`; ignored for `BROWSER`. |

Behavioral details:
- For `loginOption: 'AGENT_DN'`, the SDK validates the dial number. If invalid, the promise rejects with an error indicating `INVALID_DIAL_NUMBER`.

#### Response Payload

On success, the resolved data includes a media profile summary and login details.

| key | description |
| --- | --- |
| `deviceType` | The device type used for the login (`BROWSER`, `EXTENSION`, or `AGENT_DN`). |
| `dn` | The directory number used/assigned for the session (if applicable). |
| `auxCodeId` | Aux code id applied at login time (defaults to `0` in many deployments). |
| `lastStateChangeTimestamp` | ISO timestamp of the last agent state change. |
| `lastIdleCodeChangeTimestamp` | ISO timestamp of the last aux code change. |
| `mmProfile` | Media profile summary for the session (object). |

#### Success & Failure events

```javascript
webex.cc.on('agent:stationLoginSuccess', (data) => {
  // Update UI with deviceType, dn, auxCodeId, timestamps, etc.
});

webex.cc.on('agent:stationLoginFailed', (error) => {
  // Inspect error for input validation or other failures (e.g., error.data.fieldName, error.data.message)
});
```
