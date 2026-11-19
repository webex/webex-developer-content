---
type: Guide
title: Webex Contact Center Web SDK | Authentication
display_title: Authentication
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication)

This guide covers authentication; session registration and cleanup; agent station login and logout; automatic relogin; multi-login behavior; and agent state management in the Contact Center SDK.

---



> **Info**
>
> Note: For single-session apps, you can rely on method promises alone, subscribe to events mainly for multi-session support (for example, handling more than one active session).

<br>

## Prerequisites

- A Webex access token (via OAuth or an access token string).
- Initialize the SDK with your token using `Webex.init()` as mentioned in the [Quickstart Guide](https://developer.webex.com/docs/sdks/contact-center/quickstart-guide.md).

Optionally, you can control Contact Center plugin behavior via configuration flags:
- `allowMultiLogin` (default: true)
- `allowAutomatedRelogin` (opt-in)

## Session Registration and Cleanup

### Register

Establishes the connection to Contact Center services and fetches the agent profile.

```javascript
await webex.cc.register();
```

#### Request Parameters

None.

#### Response Payload

| key | description |
| --- | --- |
| `agentId` | Unique identifier for the agent. |
| `agentName` | Display name of the agent. |
| `teams` | Array of teams the agent belongs to. Each item includes at least `id` and `name`. |
| `defaultDn` | Default directory number configured for the agent. |
| `dn` | Current directory number assigned to the agent (may be empty if not applicable). |
| `webRtcEnabled` | Whether browser-based calling (`BROWSER`) is enabled for the agent. |
| `loginVoiceOptions` | Allowed login device types for the agent. Values may include `BROWSER`, `EXTENSION`, `AGENT_DN`. |
| `wrapupCodes` | Array of wrap-up codes available to the agent. Each item includes `id` and `name`. |
| `idleCodes` | Array of idle (aux) codes available to the agent. Each item includes `id`, `name`, and `isSystem`. |
| `lastStateAuxCodeId` | Aux code id associated with the agent’s last state. |
| `lastStateChangeTimestamp` | ISO timestamp of the last agent state change. |
| `lastIdleCodeChangeTimestamp` | ISO timestamp of the last aux code change. |
| `outDialEp` | Entry point id to use for outdial. |
| `isAgentLoggedIn` | Whether the agent is already logged in on a station. |



> **Info**
>
> Note: If `allowAutomatedRelogin` is enabled at init, the SDK can perform an automatic relogin when needed.

<br>

### Deregister

Closes sockets, removes listeners, and clears cached agent configuration.

```javascript
await webex.cc.deregister();
```

#### Request Parameters

None.

#### Response Payload

None. The operation completes when resources are released.



> **Info**
>
> Note: This does NOT perform a station logout. If you want the agent to log out, call the `stationLogout()` method first.

<br>

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

## Agent Logout

```javascript
await webex.cc.stationLogout({ logoutReason: 'logout' });
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `logoutReason` | string | no | Optional free-text or enumerated reason. Common value: `logout`. |

#### Response Payload

None. The operation completes when the station is logged out.

#### Success & Failure events

```javascript
webex.cc.on('agent:logoutSuccess', () => {
  // Station logout completed; update UI state
});

webex.cc.on('agent:logoutFailed', (error) => {
  // Handle failure
});
```

## Agent State: Available and Idle (Aux Codes)

Change the agent state using `setAgentState`:

```javascript
await webex.cc.setAgentState({
  state: 'Available' | 'Idle',
  auxCodeId: '<AUX_CODE_ID>',
  lastStateChangeReason: '<FREE_TEXT_REASON>',
});
```

#### Request Parameters

| key | type | required | description |
| --- | --- | --- | --- |
| `state` | string | yes | Target state. One of `Available` or `Idle`. |
| `auxCodeId` | string | conditional | Required when `state` is `Idle`; commonly `'0'` represents Available. |
| `lastStateChangeReason` | string | no | Optional free-text reason to accompany the change. |
| `agentId` | string | no | Optional; when provided, targets a specific agent id. Defaults to the current agent. |

#### Response Payload

None. Use events to react to the resulting state.

#### Success & Failure events

```javascript
webex.cc.on('agent:stateChangeSuccess', (data) => {
  // Make UI changes as per auxCodeId and timestamps
});

webex.cc.on('agent:stateChangeFailed', (error) => {
  // Handle failure
});
```

## Relogin (Silent Relogin)

When `allowAutomatedRelogin` is enabled during `Webex.init`, the SDK can automatically relogin if the agent already has an active session.

#### Request Parameters

None (automatic behavior).

#### Response Payload

Delivered via the success event payload.

| key | description |
| --- | --- |
| `deviceType` | The device type the agent is logged into (`BROWSER`, `EXTENSION`, or `AGENT_DN`). |
| `dn` | The directory number used/assigned for the session (if applicable). |
| `auxCodeId` | Aux code id applied to the agent at the time of relogin. |
| `lastStateChangeTimestamp` | ISO timestamp of the last agent state change. |
| `lastIdleCodeChangeTimestamp` | ISO timestamp of the last aux code change. |

#### Success event

```javascript
webex.cc.on('agent:reloginSuccess', (data) => {
  // Automatic relogin completed; update UI (deviceType, dn, aux code, timestamps)
});
```

## Multi-Login Behavior

The plugin supports a multi-login flag:
- `allowMultiLogin` (default: false)

If another session is detected for the same agent and the `allowMultiLogin` flag is `false`, the SDK emits:
- `agent:multiLogin`

The consuming application can use this event to prompt the user to close one of the sessions or to take other appropriate action -

```javascript
webex.cc.on('agent:multiLogin', (data) => {
  // Another session detected; prompt the user or close one session
});
```

## Putting It Together: Minimal Flow

```javascript
// 1) Initialize Webex with token and (optionally) CC plugin flags
const webex = Webex.init({
  config: {
    cc: { allowAutomatedRelogin: true, allowMultiLogin: true },
  },
  credentials: { access_token: token }
});

// 2) Register
const profile = await webex.cc.register();

// 3) Login (choose device type)
await webex.cc.stationLogin({
  teamId: profile.teams[0].id || profile.teams[0].teamId, // use the appropriate team identifier from the profile
  loginOption: 'BROWSER',
  dialNumber: ''
});

// 4) Set state to Available (auxCodeId '0' is a common default)
await webex.cc.setAgentState({ state: 'Available', auxCodeId: '0', lastStateChangeReason: 'Manual' });

// 5) Later: Logout and/or Deregister
await webex.cc.stationLogout({ logoutReason: 'logout' });
await webex.cc.deregister();
```

## Events to handle

From the SDK emissions:
- As mentioned before, in single-session flows, these events are not required; you can rely on the resolved/rejected promises of the API calls. 

- `agent:stationLoginSuccess`: Fired after successful station login.
- `agent:stationLoginFailed`: Fired if station login fails.
- `agent:logoutSuccess`: Fired after successful station logout.
- `agent:logoutFailed`: Fired if station logout fails.
- `agent:stateChange`: Fired for generic agent state change notifications.
- `agent:stateChangeSuccess`: Fired when state change succeeds.
- `agent:stateChangeFailed`: Fired when state change fails.
- `agent:reloginSuccess`: Fired after an automatic relogin completes (when enabled).
- `agent:multiLogin`: Fired when multiple logins are detected for the same agent.
