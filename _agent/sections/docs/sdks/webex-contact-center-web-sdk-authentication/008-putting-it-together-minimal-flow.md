---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-authentication
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Putting It Together: Minimal Flow'
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
