---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Events to handle
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
