---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 1: ''Webex for Developers'' documentation'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman). [Full Markdown](../../../../docs/create-spaces-add-participants-post-messages-from-postman.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Selected section

## Step 1: 'Webex for Developers' documentation

If you are new to Webex APIs, **Webex for Developers** is the place you'll want to start from: the portal exposes the reference documentation for the REST API, and the developer SDKs available to extend Webex.

1. Login at [Webex for Developers](https://developer.webex.com).

    > Note that you will not need to create a separate developer account. The same user account lets you access both Webex clients and 'Webex for Developers'

1. Once logged in, grab a temporary developer access token for your account by navigating to the [**Accounts and Authentication** section](https://developer.webex.com/docs/api/getting-started#accounts-and-authentication) of the **Getting Started** page:

    Copy your developer access token and save it in a safe place, as you'll be using the token in later steps of this tutorial:

    ![Developer Access Token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte72286f5ecee0087/61df5218dea73a236fc578ab/spark_access_token.png)

    > Note that your developer access token is provided for test purposes only - never use it in production. 
The token expires 12 hours after being generated, or upon logging out of 'Webex for Developers'. If your personal token is compromised, simply logout and sign in again on the developer portal to invalidate any previous tokens.

1. On that same page, scroll down and click the '+' icon next to **Full API Reference** in the left navigation panel to expand the API references. Check the various API resources entries in the table of contents:

    ![API Resources](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1f628059c6493986/61df51c51009c9654aca6b26/api-toc.png)

    These resources let you interact with spaces and receive notifications as users interact in Webex. The table below gives you a quick overview of some of the basic features offered by the Webex API resources:

    ![API Resources detailed](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbf77cde571168a12/61df51c5ef206c6c5e494d4d/api-resources.png)

1. Scroll down the API reference items and click on [Rooms](https://developer.webex.com/docs/api/v1/rooms) to access the documentation for the API used for managing spaces. The following is the URL we will use for accessing it from the REST client:
    ```shell
    https://webexapis.com/v1/rooms
    ```

    > *Note*: Webex *rooms* were renamed *spaces*. However, the Webex API still uses the `/rooms` resource, and room identifiers properties named `roomId`. Throughout these tutorials, you may see the 'Space' and 'Room' terms used interchangeably.

1. The 'Webex for Developers' API documentation is interactive: click the 'List Rooms' method on the [Rooms](https://developer.webex.com/docs/api/v1/rooms) page to view documentation for the API resource and try out sample requests. Make sure **Try It** mode is enabled to send HTTP requests and get instant responses from the Webex REST API right in your browser:

    ![Try It Mode](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt378df3c56a50969b/61df52182e109d6c649d470e/test-mode.png)
