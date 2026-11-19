---
type: Guide
title: Access the Webex API
display_title: Access the API
canonical_url: https://developer.webex.com/docs/getting-started
content_type: documentation
product_group:
- webex-suite
- webex-contact-center
categories:
- admin
- calling
- create
- meeting
- messaging
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/getting-started)

The Webex APIs give you easy access to the Webex Platform to build [Bots](https://developer.webex.com/docs/bots) or [Integrations](https://developer.webex.com/docs/integrations). If you're ready to start using the Webex APIs, keep reading.



To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/getting-started>) and sign in.



## What's possible with the Webex APIs?

The Webex APIs provide your applications with direct access to the Cisco Webex Platform, giving you the ability to:

* [Create a Webex space and invite people](https://developer.webex.com/docs/api/v1/rooms)
* [Search for people in your company](https://developer.webex.com/docs/api/v1/people)
* [Post messages in a Webex space](https://developer.webex.com/docs/api/v1/messages)
* [Get Webex space history](https://developer.webex.com/docs/api/v1/messages/list-messages) or be [notified in real-time](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook) when new messages are posted by others
* [Execute a command on a Webex RoomOS device](https://developer.webex.com/docs/api/v1/xapi/execute-command)
* and much more!

## Accounts and Authentication

To use the Webex REST API you'll need a Webex account backed by Cisco Webex Common Identity (CI). If you already have a Webex account, you're all set. If you're using Webex Meetings, your site will [need to be on Common Identity](https://help.webex.com/WBX000023841/).

If you don't already have a Webex account, go ahead and [sign up](https://www.webex.com/pricing/free-trial.html)! You'll need an account to use the APIs and SDKs.

When making requests to the Webex REST API, an `Authorization` HTTP header is used to identify the requesting user. This header must include an access token. This access token may be a [personal access token](https://developer.webex.com/docs/getting-your-personal-access-token), a [Bot](https://developer.webex.com/docs/bots) token, or an OAuth token from an [Integration](https://developer.webex.com/docs/integrations).

## Personal Access Tokens

A personal access token is a short-lived access token you can use to make Webex API calls on your own behalf. Any actions taken through the API will be done as you. Personal access tokens expire 12 hours after you sign in to the Developer Portal and should not be used in production environments. A production app should instead create an [integration](https://developer.webex.com/docs/integrations) to obtain an access token from an authenticating user using OAuth.

To get your personal access token:

1. Make sure you're [signed in](https://developer.webex.com/login) to the Developer Portal.
2. Click the copy icon below.

    

To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/getting-started>) and sign in.



3. Click OK in the dialog to copy the token to your clipboard.

    ![Copy token dialog](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf5b1cebd6cfc67d4/632b8795dbb41c0cdadc8431/copy-token.png)

## Methods & Content Types

The Webex APIs are RESTful. In REST, each resource is represented by a base URL like `/messages` and the HTTP methods `GET`, `POST`, `PUT` and `DELETE` are used to request data and perform actions on those resources.

For methods that accept request parameters the platform accepts either `application/json` or `application/x-www-form-urlencoded` content types and currently only supports returning data in `application/json` format.

## Next Steps

Continue through the API access and authorization journey:

1. Read [Authentication](https://developer.webex.com/docs/authentication) to understand access tokens and the OAuth authorization flow.
2. Get a [Personal Access Token](https://developer.webex.com/docs/getting-your-personal-access-token) to test API requests with your own Webex account.
3. [Create an Integration](https://developer.webex.com/docs/integrations) when your application needs to access Webex on behalf of other users.
4. Review [Integration Scopes](https://developer.webex.com/docs/integration-scopes) and request only the permissions your application needs.

Then browse the API endpoints under **Reference** in the left navigation. When you find an endpoint that fits your use case, open it and try the request in your browser.

If you prefer tutorials and structured lessons definitely check out the [Learning Labs](https://learninglabs.cisco.com/tracks/collab-cloud) by Cisco DevNet.

Once you've learned the APIs and are ready to build an app you may be interested in using an SDK to eliminate some boilerplate. Check our list of SDKs over in the menu on the left side of this page. If your favorite language isn't listed don't worry, SDKs in new languages will be added regularly.

## Support Policy

Please visit the [Webex API and SDK Support Policy](https://developer.webex.com/docs/api-and-sdk-support-policy) page for details on our support and end of life policy for APIs and SDKs.

## Getting Help

If you ever get stuck, the [Webex Developer Support team](https://developer.webex.com/support) has you covered, standing by 24/7 to help.
