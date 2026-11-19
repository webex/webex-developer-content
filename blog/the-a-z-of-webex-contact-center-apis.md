---
type: Article
title: 'The A-Z of Webex Contact Center APIs: Capture APIs'
canonical_url: https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis
content_type: blog
date: '2025-08-04'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis)

<iframe src="https://app.vidcast.io/share/embed/b0b80853-df73-4613-9761-7b8ca0a83153?disableCopyDropdown=1" width="100%" height="100%" title="Captures API" loading="lazy" allow="fullscreen;autoplay;" style="position: absolute; top:0; left: 0; border: solid; border-radius: 12px;"></iframe>


As a reader of this blog, hopefully you are continuing a journey of another installment of the blog series, “[The A-Z of Webex Contact Center APIs](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-audio-files)”. This time we are talking about capturing Task recordings that become available to developers via the Webex Contact Center Captures API. According to the Webex developer documentation, a “Task represents a request or demand for attention/work from agents. Concretely, a telephony Task is an incoming call. For chat, a Task is a chat session. For email, a Task is an email chain.” The data associated with actions performed by Webex Contact Center agents are often recorded and stored by Webex and made available to developers that have access to various APIs that consume the data. Below we will explore how to leverage the Captures API to do things like get telephony recordings and email transcripts.

### Webex Contact Center Developer Sandbox

A good place to start when developing apps that work with the Webex Contact Center is with requesting a [Webex Contact Center Developer Sandbox](https://developer.webex.com/webex-contact-center/docs/sandbox_cc). This tool provides developers with an org that they can use to provision up to 10 licensed Webex users of various roles. They can then generate content in the sandbox and build applications without worrying about whether they are going to disrupt the operations of an org that is handling customer support in real time. Freely build and break things without consequence by logging into the developer portal and requesting a sandbox today!

### Register a Client Application

Webex provides developers with two client application types to employ when leveraging the Captures APIs. One option a developer can go with is a Webex Contact Center Integration and the other is a Webex Contact Center Service App.

#### Webex Contact Center Integrations

A [Webex Contact Center Integration](https://developer.webex.com/docs/integrations) requires the developer to implement an [OAuth 2.0 flow](https://developer.webex.com/docs/authentication) using the provided client credentials. Once a user authorizes the client application to make API requests on their behalf, the developer can get an access token to start gathering a Webex Contact Center organization’s historical recording data, and setting the proper webhooks to get notified when new recordings become available. Here are several caveats to think about in this scenario. The user that authorizes the app in the OAuth 2.0 flow has to be an administrator with the proper permissions to make API calls that align with either the `cjp:config_read` or `cjp-analyzer:read` scopes, and others. To initiate this flow, which is manual, you typically need to present a web page or button to "Connect with Webex".

#### Webex Contact Center Service Apps

A [Webex Contact Center Service App](https://developer.webex.com/create/docs/service-apps) is like a Integration in that the goal of obtaining an access token to make API calls is the same, but the mechanism for obtaining the access token is not dependent on the developer having a user interface for a user to kick off an OAuth 2.0 flow, instead the Service App is approved by an administrator in Control Hub. Also, when a developer ultimately gets an access token to use in their client application, they are not making API calls on behalf of a single user or administrator as is the case with an Integration leveraging OAuth 2.0. The Service App is a virtual admin and is recognized by Webex services as a machine account. This virtual admin can perform administrator tasks through the Webex Contact Center APIs. Any administrator with access to the control hub can authorize a Service App by navigating to the Control Hub’s Application section given they have matching permissions that align with the [scopes](https://developer.webex.com/create/docs/integrations#scopes) that the developer selected when registering the Service App.

One caveat here is that for a developer who wants to productize their Service App and make it available to any Webex user that has access to the Control Hub, they would need to submit and publish the Service App on the [Webex App Hub](https://apphub.webex.com/). Alternatively, an in-house developer could register the Service App and make the app available to the admin for the organization they belong to by requesting the administrator’s approval from the Service App’s page in the developer portal.

Once an app is approved by an administrator the developer can obtain the access token and refresh token in the Webex Developer Portal or build a separate [client integration](https://github.com/WebexSamples/service_app_token_getter) to automate the token retrieval process via API. Since the access token turns the Service App into a Virtual Admin, the developer can set the scopes for the token to include the required `cjp:config_read` or `cjp-analyzer:read` as required by the Captures API set.

#### Captures APIs

Let’s break down the API endpoints that make capturing Task and recording data happen:

#### Captures Webhook

[https://api.wxcc-us1.cisco.com/v2/subscriptions](https://api.wxcc-us1.cisco.com/v2/subscriptions)

The first thing a developer may want to do, once they have obtained an access token, is to set [webhooks](https://developer.webex.com/webex-contact-center/docs/webhooks-cc) that will instruct Webex services to let the client application know when a new recording or Capture is available. This can be accomplished leveraging the [Subscriptions API](https://developer.webex.com/webex-contact-center/docs/api/v1/subscriptions). This API can monitor several event types, but to stay on topic for this blog we will focus on the Captures event, capture:available. In the body of an API request to this endpoint, the developer is required to name the webhook, provide the events we are subscribing to (Captures in this case) in the event type parameter, include an orgId, and a resource version. The resource version can be obtained by using the List Event Types API.

The event payload that the client application receives when this webhook is triggered will include a taskId and a link to the downloadable recording. The Subscriptions API for webhooks requires `the cjp:config_read` or `cjp:config_write scopes`.

#### List Event Types

This API should be used to get the resource version data that is needed in the Captures Webhook/Subscription API request. Requires `cjp:config_read` scope.

#### List Captures

[https://api.wxcc-us1.cisco.com/v1/captures/query](https://api.wxcc-us1.cisco.com/v1/captures/query)

This is the API that has the recording and Task data that most developers looking at this blog is interested in. Initially, a developer may want to call this after setting hooks so that they can store any available historical recording and Task data.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
