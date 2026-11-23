---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Session Registration and Cleanup
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
