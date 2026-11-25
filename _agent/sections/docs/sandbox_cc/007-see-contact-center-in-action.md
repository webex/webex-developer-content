---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sandbox_cc
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- See Contact Center in Action
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sandbox_cc). [Full Markdown](../../../../docs/sandbox_cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

To request or manage a Contact Center sandbox, open the [official portal page](<https://developer.webex.com/docs/sandbox_cc>) and sign in.

## Selected section

## See Contact Center in Action

Now that you’ve got your sandbox up and running, let’s get it configured so you can see Webex Contact Center in action.

### Prerequisites

Before continuing, make sure you have access to the following:

- A machine that can run the Webex Contact Center Desktop, as well as the [Webex app](https://www.webex.com/downloads.html) (you can also use the [Webex Calling plug-in](https://chrome.google.com/webstore/detail/webex-calling-for-chrome/llllflgakifpdcmoanonghipldcpaggn) for Chrome). You’ll use this as your virtual "call center agent."
- A second separate machine running the Webex application, a [supported physical device](https://help.webex.com/en-us/article/n9r1aac/Configure-and-manage-Webex-Calling-devices) (you can log in with your own Webex ID), or, really, any phone system. This will be your virtual "Customer" calling in for support.

### Set up Your Contact Center

To configure your Webex Contact Center system:

1. On your first physical machine, set up your first agent (either the Premium Agent or the Supervisor) to login to the Webex app.
1. On the same machine, log the same agent into Webex Contact Center Desktop: [https://desktop.wxcc-us1.cisco.com](https://desktop.wxcc-us1.cisco.com).
1. When you log in, enter the Extension for the agent as specified in your provisioning email.

    **Note:** If you choose to use the Supervisor account make sure you set the role to both **Agent and Supervisor** so the account can receive calls.

1. Change the agent’s status to **Available**.
1. On your second physical machine, login to either the Webex app or a [supported physical device](https://help.webex.com/en-us/article/n9r1aac/Configure-and-manage-Webex-Calling-devices). If all you’ve got is a cell phone or a desk phone, there’s nothing to configure.

### Test Out Your Call Center

To test out your call center:

Make sure that you’ve got handy access to the machine to host the logged in Contact Center agent. You’ll need to manually answer unless you’ve got a cooperative friend available.

**Note:** Remote desktop software works well for this purpose.

From your normal Webex account, your Webex-enabled device, or any other standard PSTN phone, place a call to the **Entrypoint** number specified in your provisioning email.

You’ll hear the default greeting which will tell you to make sure you’ve got an agent logged into the Agent Desktop. You’ll then be placed in the queue with the default hold music playing.

Switch to the machine running the Agent Desktop and answer the incoming call notification. If you’ve got someone posing as the call center agent, you can chat—the call itself is being recorded.

Terminate the call from either end whenever you like. The agent will be prompted with a **Wrap Up Reasons** dialog (containing only a single option, **Sale**). Select the option and select **Submit Wrap Up**.

**Note:** For details on using the Agent Desktop, see the [Agent Desktop Help System](https://desktop.wxcc-us1.cisco.com/help/#!webexcc_g_30-introduction.html).
