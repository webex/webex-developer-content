---
type: Excerpt
canonical_url: https://developer.webex.com/docs/instant-connect-meeting-links
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/instant-connect-meeting-links). [Full Markdown](../../../../docs/instant-connect-meeting-links.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This guide shows how you can construct Instant Connect URLs for hosts and guests.

---

Using a simple REST API, you can easily generate Instant Connect URLs for one or multiple hosts and guests. The API allows for a variety of customizations via its request payload, including:

- A configurable meeting subject
- Not before and expiration times for the authorization JWT
- Device support
- Parameters to set the number of hosts and guests up to a maximum of 25 each
- An option to generate short URLs
- Various advanced encryption options

The guide includes a step by step example using Postman, if you're new to REST APIs. Alternatively, if you're a REST veteran, you can skip directly to the API Reference materials at the end of this document.

## Selected section

## Prerequisites

Before you can use Instant Connect, your Webex Admin will need to login to the Instant Connect webpage and choose **Activate Instant Connect** here:<https://instant.webex.com/integrate/>.



> **Info**
>
> You only have to activate Instant Connect once.



Next, you'll need to generate an access token which is required to make the API call to retrieve the encrypted part of the URLs. You've got two options for access tokens:

- A 12 hour time limited Personal Access token for development purposes
- A 100 year Bot token for production use

In addition, optionally, to enable adding devices to the meeting, you'll need to configure Instant Rounding as described in the following help.webex.com article [Configure Virtual Rounding](https://help.webex.com/article/6vsdoi/).

### Retrieve a Personal Access Token for Development

To obtain a Webex Personal Access Token (valid for 12 hours), navigate to the [Webex Developer Portal](https://developer.webex.com/docs/getting-started#accounts-and-authentication), login with your Webex org admin account, and copy the Bearer token value:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt84e562902cf23694/63c03de3d2d671109381b574/01-personal-token.png)

### Retrieve a Bot Token for Production Usage

For a production-level implementation, we recommend [creating a new Webex Bot](https://developer.webex.com/my-apps/new/bot) and using the Bot’s access token (valid for 100 years). You can copy the Bot access token once you've created your new bot:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8125b962e4bdceda/63c03de3def66d1d64a3b768/02-bot-token.png)
