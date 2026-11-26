---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-your-own-jira-server-bot-integrated-with-webex
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-your-own-jira-server-bot-integrated-with-webex). [Full Markdown](../../../../docs/create-your-own-jira-server-bot-integrated-with-webex.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This article explains how you can create your own Webex-integrated Jira Server bot.

## Selected section

## Build the Bot

Before Jira Server non-admin users can use your bot, you need an authentication process in your bot to communicate with Jira. For this you will need to create an application link in Jira. You must complete the steps below using your Jira administrator account.

For additional information, refer to this link for OAuth authentication steps <https://developer.atlassian.com/cloud/jira/software/scopes-for-oauth-2-3LO-and-forge-apps/> as well as [atlassian-oauth-examples](https://bitbucket.org/atlassianlabs/atlassian-oauth-examples/) repository to learn how to create an OAuth client.

1. Note down the Jira Server base URL required following steps:
    If your Jira Server account URL is `https://sample.acme.com`, for example, then `sample.acme.com` is the base URL.
1. Sign in to your Jira Server account as an administrator:[https://id.atlassian.com/login](https://id.atlassian.com/login).
1. Select the **Settings** icon and then choose **Applications**:
1. In the left pane, under **Applications** select **Application links**.
1. Enter any URL of your choice into the input field and then select **Create new link**. The actual URL doesn’t matter because it's only retrieving data from Jira.
1. On the first screen in **Link applications**, enter the following details:
    - **Application name**: Enter a name for your application.
    - **Application type**: Select Generic Application.
    - **Service Provider Name**: Enter anything.
    - **Consumer key**: Enter anything.
    - **Shared Secret**: Generate a private key using: [https://docs.openssl.org/master/](https://docs.openssl.org/master/).
    - **Request Token URL**: Use `<base URL from step 1>/plugins/servlet/oauth/request-token`.
    - **Access Token URL**: Use `<base URL from step 1>plugins/servlet/oauth/access-token`.
    - **Authorize URL**: Use `<base URL from step 1>plugins/servlet/oauth/authorize`.
1. In the next screen, enter the consumer details for the client:
    - **Consumer key**: Enter the same value from the previous screen.
    - **Consumer name**: Enter the same value from the previous screen.
    - **Public key**: Generate a public key using: [https://docs.openssl.org/master/](https://docs.openssl.org/master/).
1. Select **Continue**. The client is now configured as an OAuth consumer in Jira.
1. Log in to [Webex for Developers](https://developer.webex.com/).
1. Create your Webex bot at: [https://developer.webex.com/my-apps/new/bot](../../../../docs/my-apps/new/bot).
1. Note down the bot's access token, which you'll use to make API requests.
