---
type: Article
title: Webhooks for Service App Authorizations
canonical_url: https://developer.webex.com/blog/webhooks-for-service-app-authorizations
content_type: blog
date: '2024-10-02'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webhooks-for-service-app-authorizations)

A [Webex Service App](https://developer.webex.com/docs/service-apps) is special integration type that provides admin access to the Webex REST APIs on behalf of an organization. This lessens the reliance on an individual user's authorization and reduces risk to mission critical applications, like active reporting and compliance use cases. Webex administrators [have full control](https://developer.webex.com/docs/service-apps#service-app-creation-admin-flow) over what Service Apps are allowed in their organization.

When a Service App is *authorized* by a Webex admin, the API access tokens become available to the respective developer. That Service App can also be revoked at any time when it’s *deauthorized* by the admin. Developers can now be notified of these events with the introduction of a new [webhook](https://developer.webex.com/docs/webhooks) resource `serviceApp` and events `authorized` or `deauthorized`. This provides an automatic method to communicate Service App status changes and enable different workflows from those events. For example, if a Service App is running a critical process (such as active call reporting) and is unexpectedly deauthorized, this can trigger a workflow to send an alert to the team that depends on the reports. Let’s take a closer look at how these webhook events work.

### Register the Webhook

To be notified when a Service App is authorized or deauthorized, developers can subscribe to the new webhook resource - `serviceApp` and specify the event as `authorized` or `deauthorized`.

By default, these webhooks will notify on *all* Service App authorized or deauthorized events for that developer. To limit those event notifications to specific Service Apps or Webex sites, there are four filters available:

- `id`
    - Notify by Service App ID
- `friendlyName`
    - Notify by the Service App “friendly”name.
- `trainSiteNames`
    - Notify by Webex site names
- `adminTrainSiteName`
    - Notify by the admin Webex site name

For example, creating a webhook to notify when a specific Service App is authorized is as simple as sending a POST to the [/v1/webhooks API](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook) with the following JSON body:

```json
{
  "name": "Service Apps authorization",
  "targetUrl": "https://example.com/mywebhook",
  "resource": "serviceApp",
  "event": "authorized",
  "filter": "id=ZGYtODM3YTRmZjkxOTEw"
}
```

Notice the filter that is applied there, which tells Webex to notify only when a Service App with that `id` is `authorized` by an organization.</a> For more information on creating webhooks, check out the [developer guide](https://developer.webex.com/docs/webhooks).

### Webhook Payloads

When the above webhook is triggered by a new admin authorization for the Service App, the JSON payload received will look something like this:

```json
{
  "id": "ZGYtODM3YTRmZjkxOTEw",
  "name": "My Service App Auth",
  "targetUrl": "https://example.com/appUrl",
  "resource": "serviceApp",
  "event": "authorized",
  "orgId": "MDVhNzA1ZDcwYjQ",
  "createdBy": "Zi05YjA0MDZkZjFkOTY",
  "appId": "Njk2YWMwYTEwN2Q2YTg5MjI3",
  "ownedBy": "creator",
  "status": "active",
  "created": "2024-06-05T18:09:34.929Z",
  "actorId": "Yjk2YS03NGQ4NWYxNjU1ZmE",
  "data": {
    "id": "ZDllNzczMzllOGVlODI5OTll",
    "friendlyId": "super-special-service-app",
    "authorizerId": "Yjk2YS03NGQ4NWYxNjU1ZmE",
    "authorizerOrgId": "YTU2YS1iMDVhNzA1ZDcwYjQ",
    "authorizationDate": "2024-06-12T14:19:52.168Z",
    "scopes": [
      "spark:kms",
      "meeting:admin_schedule_write"
    ],
    "trainSiteNames": [
      "clgmaiyaaq.webex.com"
    ],
    "adminTrainSiteNames": [
      "clgmaiyaaq.webex.com"
    ]
  }
}
```

As you can see, the values that correspond to the four available webhook filters are included in the JSON payload. The payload for a `deauthorized` event will have the same data fields, making it easier to handle both events. Receiving these real-time events allows your application to perform the next steps in your development workflow!

### Need Some Help? We Got You Covered!

We are delighted to provide assistance if you need any help with these new webhooks. As always, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Until next time, happy developing!
