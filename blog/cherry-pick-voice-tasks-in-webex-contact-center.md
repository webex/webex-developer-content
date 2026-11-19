---
type: Article
title: Cherry-Pick Voice Tasks in Webex Contact Center
canonical_url: https://developer.webex.com/blog/cherry-pick-voice-tasks-in-webex-contact-center
content_type: blog
date: '2026-04-28'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/cherry-pick-voice-tasks-in-webex-contact-center)

In contact centers, sometimes supervisors or agents need a way to see what is waiting in the queue and pull the right call instead of relying on automatic distribution. This is necessary in Hospital Transfer Centers where a nurse may need to connect multiple inbound calls from clinicians.

In this post, we will walk through a small Agent Desktop widget that does exactly that for Webex Contact Center: displays queued voice calls and uses the Get Tasks and Assign Task APIs so an agent can cherry-pick a call.

### What the widget does

The project hosts a custom widget intended to run inside Contact Center Agent Desktop. A queue flow can notify the widget server side when new phone contacts arrive (optional but recommended for responsiveness). The widget uses the Contact Center APIs to list tasks the agent has access to and to assign a chosen task. Together, that gives the end user a practical pattern for “see the queue, pick the call” experiences where the queue and multimedia profile policies support manual assignment.

### How to get started

The full source for this proof of concept is [on GitHub](https://github.com/wxsd-sales/wxcc-voice-cherry-picker). For API details, start with the official [task call-control documentation](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control/get-tasks) for Webex CC.

1. **Manual assignment must be allowed**\
   For Get/Assign behavior to work as expected for voice, your service queue and the agent’s multimedia profile (MMP) need manuallyAssignable configured appropriately (queue-level flag and MMP telephony manual assignment). The repository [README](https://github.com/wxsd-sales/wxcc-voice-cherry-picker?tab=readme-ov-file#3-update-the-queue-and-mmp-manuallyassignable-properties) describes the shape of those settings; many teams apply them with an API client such as Postman or Bruno rather than in the widget code itself.


2)  **Optional flow hook for faster UI updates**\
   If you only rely on polling, new tasks appear on a several second interval. To push calls to the widget sooner, add an HTTP Request node in your queue flow POSTs to your widget server’s public URL with a JSON body containing the contact fields  described [here](https://github.com/wxsd-sales/wxcc-voice-cherry-picker?tab=readme-ov-file#2-configure-the-cc-queue-flow).


3. **Running the sample**\
   Clone the repository, copy .env.example to .env, set PORT (for example 5000) and HOST_URI to the base URL where the server will be reachable (<http://localhost:5000> for local dev, or <https://your.server.com> in production).

Full setup instructions can be found [here](https://github.com/wxsd-sales/wxcc-voice-cherry-picker?tab=readme-ov-file#1-set-up-the-env-file).

### See it in action

For a quick overview of behavior and setup, checkout the [Vidcast](https://app.vidcast.io/share/1ec61338-9263-4e20-95c7-87cb24dfbdf3)!

### In closing

If you are extending Contact Center with custom desktop experiences, this sample is a compact reference for task discovery, assignment, and flow-to-widget signaling. If you have questions about Webex APIs or SDKs, you can reach developer support at [devsupport@webex.com](mailto:devsupport@webex.com). For questions about this WXSD sales engineering sample specifically, use [wxsd@external.cisco.com](mailto:wxsd@external.cisco.com).
