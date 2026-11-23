---
type: Excerpt
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Test with the Widgets sample application
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/cc-web-widgets-components-agent-wellness-break-beta). [Full Markdown](../../../../docs/cc-web-widgets-components-agent-wellness-break-beta.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](001-before-you-begin.md)

## Article introduction

Use this guide to test Agent Wellness Break in the Cisco AI Assistant React widget. The widget shows suggestions and offers, runs the timed break after active work is complete, and returns the agent to Available.

## Selected section

## Test with the Widgets sample application

Use the beta React sample build supplied with your invitation. Confirm that it includes the versions listed above. The widget responds to live wellness events; there is no control to create a mock offer.

1. Sign in as the beta test agent and initialize the sample with a temporary developer access token. Do not put the token in a screenshot or test report.
2. Select **AI Assistant**, complete Station Login, and set the agent to **Available**. Before a wellness event, confirm that the assistant shows its landing content.
3. Wait for a wellness suggestion. Select **Take wellbeing break** once. Confirm that the request remains pending until the service approves or denies it. A later suggestion is required before another manual request is available.

    ![Cisco AI Assistant wellness suggestion with the Take wellbeing break button.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltef5b2200cafaef01/6abe90fedb047411f049d8f3/agent-wellness-widgets-suggestion.jpg)

4. Test a direct offer with the assistant open. Confirm that the offer appears in the panel. Repeat with the panel closed or minimized. Confirm that one actionable notification shows **Take a break** and **Later**.

    ![Well-being break scheduled card with Take a break and Later buttons.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75d844166811e26a/6abe907f60418e3b53b9bfcd/agent-wellness-widgets-direct-offer.jpg)

    ![Wellness notification with Later and Take a break actions.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8283cd3fa6763e30/6abe908bfd70711b0db2b411/agent-wellness-widgets-actionable-notification.jpg)

5. Select **Later** and confirm that the agent state does not change. Test an unanswered offer and confirm that it expires after five minutes without changing the state.
6. Accept a direct offer. Confirm that the agent enters `WellbeingBreak`, sees a five-second start countdown, a 60-second break, and a five-second ending countdown, and then returns to **Available**.

    ![Wellness break overlay over the React sample app with a progress indicator.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt430643953ce4a082/6abe908061afb887872409b6/agent-wellness-widgets-break-progress.jpg)

7. Accept while a voice or digital task is active. Confirm that the break waits until the task and required wrap-up finish. During the break, confirm that User State shows the timed `WellbeingBreak` state but does not list it as a selectable idle code.
8. Review wellness history. Select **Clear** and confirm that it removes displayed history without cancelling an active offer or break.
9. Test keyboard focus, reduced motion, and a blocked audio or animation request. Confirm that the break remains usable and still returns the agent to Available.
10. Repeat after logout, a station-session change, a browser refresh during the break, and a connection interruption. Confirm that stale offers do not reappear and that old-session work does not continue.

The test passes when the suggestion and offer actions work, active work delays the timer, and every completed break returns the agent to Available.
