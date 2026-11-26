---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Going further
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging). [Full Markdown](../../../../docs/using-the-webex-space-widget-for-video-and-messaging.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Going further

In this demonstration we’ve just scratched the surface of the experience the Space Widget can deliver. For example, the Space Widget can enable your web app to respond dynamically to [Widget events](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#events) (e.g. answer an incoming call),
[control the Webex features](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#configuration) that are offered in the UI, specify whether to start in messaging mode or jump directly into a video session, and more. Check out the [Widget README](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space#incoming) for all details.

In addition to basic 1-on-1 calling demonstrated in this tutorial, the Space Widget can fully participate in group/multi-user Webex meeting meetings and standard Webex meeting events, right from within your web application page.

To try this out, simply set the **Widget Destination Type** to **To Space** in the Space Widget demo app, and paste in the unique roomId of an existing Webex space.



> **Info**
>
> If you add **roomid@webex.bot** to a Space and it will automatically look-up the Space's `roomId` and send it to you in a 1-on-1 message.



![RoomId bot in action](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76657f6c544a84ae/61e8807ed4cd11754d7c2de3/roomid_bot.png)

Finally, note there is another helpful Widget we haven't even touched on yet!  Discover the [Recents Widget](https://github.com/webex/react-widgets/blob/master/packages/node_modules/@webex/widget-recents).
