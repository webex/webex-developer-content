---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Overview and limitations
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-better-together-sdk-beta). [Full Markdown](../../../../../docs/sdks/webex-better-together-sdk-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md)

## Article introduction

Use this guide to integrate and test Webex Better Together with the Webex Contact Center SDK. It lets an agent use a host application for call controls while the voice call runs in Webex App on the same computer.

## Selected section

## Overview and limitations

| Host application | Contact Center SDK | Voice client |
| --- | --- | --- |
| CRM, such as Salesforce or ServiceNow, or a custom web app | `@webex/contact-center` | Webex App desktop on the same computer, signed in as the same user |

Agents use the host application to accept or decline offers, mute or unmute an engaged call, and send keypad digits. The voice call runs in Webex App.

**Limitations for this beta:**

- Webex App hold-state synchronization is deferred; existing hold/resume controls may not match Webex App state.
- Browser/WebRTC-only station login and mobile/tablet Webex App are outside this answer flow.
- The SDK initialization flag is init-only. Changing it requires reinitializing the SDK.

For existing hold, transfer, consult, end, wrap-up, and WebRTC controls, see [Webex Contact Center SDK Tasks](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-tasks).
