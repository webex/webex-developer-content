---
type: Guide
title: Sandbox (Contact Center)
display_title: Contact Center Sandbox
canonical_url: https://developer.webex.com/docs/sandbox_cc
content_type: documentation
product_group:
- webex-contact-center
categories:
- app-hub
- create
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sandbox_cc)

To request or manage a Contact Center sandbox, open the [official portal page](<https://developer.webex.com/docs/sandbox_cc>) and sign in.



## Introduction

A Contact Center Developer Sandbox provides you with administrator access to a licensed Webex Contact Center sandbox. The sandbox lets you create and test the capabilities of the Webex Contact Center platform that are not available with Webex free plans.

To use the sandbox, you'll first need to be signed into the Webex Contact Center Developer Portal. If you don't have an account, you can create a new, free Webex account. Once your account is activated, sign in to proceed.

**Caution:** When signing into the Webex Contact Center Portals, we recommend using the latest desktop version of Google Chrome or Mozilla Firefox. Other browsers may produce unexpected results. Webex Contact Center Portals are **NOT** designed for mobile devices.

**NOTE: All sandboxes have a validity period of 180 days. Please reach out to [Developer Support](https://developer.webex.com/explore/support) to extend the validity of your sandbox.**

### Sandbox Vidcasts

For guided video introductions to requesting and provisioning Contact Center sandboxes, you can also see:

- [Provision a Contact Center Developer Sandbox](https://app.vidcast.io/share/396869f8-726e-43b8-8a10-b99016c781c3)
- [How to make your first phone call to the agent desktop](https://app.vidcast.io/share/dd5ea6e0-f3e9-4b5a-a1b0-73d76532ca33)

## Sandbox Contents

Every sandbox requested from the developer portal has the following features configured so that you can test all Contact Center features end to end:

1. **Webex calling for Voice** - Webex calling is the default calling platform. You use the main PSTN number as the entry point for contacting an agent logged into the Agent Desktop. The main PSTN number can be found in your sandbox provisioning email.
1. **Administrator** - One (1) administrator user is configured. Details are available in your sandbox provisioning email.
1. **Desktop Profiles** – Two desktop profiles are created, one with and one without auto-wrap-up enabled (the auto-wrap-up profile ends the call with a default wrap-up code rather than requiring an agent choice).
1. **Agents/Users** – Two default user are configured:

    - Premium Agent 1 who only has access to Agent Desktop functions.
    - Supervisor Agent 2 who has access to additional supervisory metrics and functions.

    Details are available in your sandbox provisioning email.

1. **Team** - A default agent-based team is available for use.
1. **Multimedia profile** - One (1) default multimedia profile is available.
1. **User profiles** - Five (5) pre-configured [user profiles](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges) are available:

    - Administrator Only Profile
    - Administrator Profile
    - Premium Agent User Profile
    - Standard Agent User Profile
    - Supervisor Profile

1. **Queue** - One (1) inbound voice queue is preconfigured.
1. **Audio files** - Default hold music as well as a greeting message are preconfigured.
1. **Flow** - A default basic flow is configured to play a default hold music and redirect the call to the default inbound queue.
1. **Business Hours** – Business hours (defined collections of operational hours enabling you to route calls to agents who are actually in the office) have been mapped to the default inbound entry point and the default basic flow that is active for 60 days from the time of creation.

## Request a Sandbox (Customers Without a Contact Center Enabled Organization)

To request a Webex Contact Center sandbox if you’ve got a regular Webex account:

1. Sign into your Webex account. If you don’t have an account, you’ll need to create one (they’re free).
1. Select **Request a Sandbox**.
1. When the request dialog appears, copy the generated ticket text.
1. Select **Create a Request Ticket**, paste the copied text into the **Description** field, and fill out the other required fields.
1. Select **Submit**. Sandbox creation may take up to 24 hours.
1. You’ll receive several emails. Check the final email for the account credentials for your admin and user accounts.

    **Note:** You can ignore the account activation emails.

## Request a Sandbox (Customers with a Contact Center Enabled Organization)

To request a new Webex Contact Center sandbox if you’re a member of a Contact Center enabled organization:

1. Sign into your Webex account.
1. Click on **Request a Sandbox** at the top of this page.

    If you already have sandboxes, you’ll see **Manage Sandbox** instead.

    If you’ve already got ANY Webex sandboxes, you’ll need to delete them before you can create a new Contact Center sandbox. Once you’ve deleted your sandboxes, continue to the next step.

    **Note:** Sandbox deletion can take up to 15 minutes.

1. Read and accept the **Terms and Conditions**, check **By creating this app, you accept the Terms of Service**, and select **Request a Sandbox**.

1. Select **Close** in the confirmation dialog.

1. You’ll receive several emails. Check the final email for the account credentials for your admin and user accounts. Sandbox setup can take up to 15 minutes.

    **Note:** You can ignore the account activation emails.

## Sandbox Provisioning Email

Once your sandbox has been created, you’ll receive a final provisioning email with important account information.

**Caution:** Make sure you save this email for future reference or record the information in a handy location.

The provisioning email contains the following information:

**Webex Site and Administrator Credentials**

- **Name**: `xxxxxx-xxxx`
- **DNS Domain**: `xxxxxxx-xxxx.wbx.ai`
- **Username**: `admin@xxxxxx-xxxx.wbx.ai`
- **Password**: `********`
- **Webex Site URL**: `xxxxxx-xxxx.webex.com`

**Two Contact Center users**

*A premium agent*

- **Username**: `user1@xxxxxx-xxxx.wbx.ai`
- **Password**: `********`
- **Extension**: `1001`

*A supervisor agent*

- **Username**: `user2@xxxxxxx-xxxx.wbx.ai`
- **Password**: `********`
- **Extension**:&#xa0;`1002`

**Two PSTN Numbers**

- A main number -&#xa0;`+1nnnnnnnnnn` - Assigned to the default location for Webex calling. This is reserved.
- An entrypoint number - `+1nnnnnnnnnn` - Assigned to the Contact Center default inbound entrypoint.

## Webex Control Hub Access

While you don’t have to make any changes in Webex Control Hub to use your sandbox, you can still log in to customize Contact Center settings, view metrics, and much more.

To access Webex Control Hub using the administrator account:

1. Close and reopen a fresh private/incognito window (Firefox Win/Mac **Ctrl+Shift+P**, Chrome Win/Mac **Ctrl+Shift+N**).
2. Copy and paste this URL into the browser and press **Enter**: [https://admin.webex.com](https://admin.webex.com)
3. Enter the administrator email address from your provisioning email.
4. Manually enter the password for your administrator account from the provisioning email.

For information on administering Webex Contact Center, see [Webex Contact Center Documentation](https://help.webex.com/en-us/article/n2re5jy/Webex-Contact-Center-Documentation).

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

## Sandbox Support

If you encounter any problems using your Contact Center sandbox, please contact us via the [Support](https://developer.webex.com/support) page.
