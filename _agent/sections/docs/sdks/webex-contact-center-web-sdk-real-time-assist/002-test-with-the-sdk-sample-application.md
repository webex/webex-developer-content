---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Test with the SDK sample application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-real-time-assist). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-real-time-assist.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Real Time Assist with the Webex Contact Center SDK. Start with the sample application, then add the request, response, and feedback handling to your application.

## Selected section

## Test with the SDK sample application

Run this test first. If it fails, fix the organization or agent setup before changing your application.

1. Open the [Webex Contact Center SDK sample application](https://webex.github.io/webex-js-sdk/samples/contact-center/).
1. Initialize the SDK with the test agent's access token.
1. Register the agent, complete station login, and change the agent state to **Available**.
1. Start and accept an incoming voice interaction.
1. Request Real Time Assist and confirm that a suggested response is received for the active interaction.
1. Add context and request another response.
1. Test the like, dislike, and copy actions on the response.

The setup is ready when the sample application receives responses for the active interaction and all three feedback actions complete without an error.

Watch the following demonstration of this flow.

<iframe src="https://app.vidcast.io/share/embed/6c256ddc-8947-4301-9ed6-52bfa25d2ef3" width="100%" height="582" title="Test Real Time Assist with the Webex Contact Center SDK sample application" frameborder="0" loading="lazy" allowfullscreen></iframe>

If the embedded video does not load, [open the SDK sample application demonstration in Vidcast](https://app.vidcast.io/share/6c256ddc-8947-4301-9ed6-52bfa25d2ef3).
