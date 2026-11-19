---
type: Article
title: Picking the Right Scopes with Webex Calling OAuth Integrations
canonical_url: https://developer.webex.com/blog/picking-the-right-scopes-with-webex-calling-oauth-integrations
content_type: blog
date: '2023-03-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/picking-the-right-scopes-with-webex-calling-oauth-integrations)

	<iframe src="https://app.vidcast.io/share/embed/0020d7a1-ff01-42dc-a225-17e4ca09b1e3" width="100%" height="100%" title="Webex Calling API Scopes" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>


When building an OAuth Integration, a scope is a mechanism that allows a user to grant limited access to their resources to a third-party application. Scopes specify what actions an application can perform on behalf of the user.

When a user is asked to grant access to their resources, they are shown the scopes that the application is requesting. The user can then decide whether to grant access to each scope.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd099945a64e745dd/641dba8088d0e31cbe08825c/picking-the-right-scopes-with-webex-calling-oauth-integrations-2.png)

For example, a social media application might request access to a user's public profile, friends list, and posts. Each of these actions could be represented by a separate scope, allowing the user to grant or deny access to each one individually. Scopes are an important security feature of OAuth because they allow users to control which parts of their resources are accessible to third-party applications.

### Webex Scopes

Webex provides a range of APIs that can be used to build integrations and applications. These APIs can be used to create custom experiences and automate workflows within Webex. 

When creating a [Webex Integration](https://developer.webex.com/docs/integrations) on the [Webex Developer Portal](https://developer.webex.com/), you will be required to choose which scopes your [integration](https://developer.webex.com/my-apps/new/integration) needs.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcfb04cb56c6d5841/641dba805c57e610a112874b/picking-the-right-scopes-with-webex-calling-oauth-integrations-3.png)

Some of the key scope areas available for Webex APIs include:

- **Meetings**: These scopes allow you to create, update, and manage meetings within Webex.
- **People**: These scopes allow you to access and manage user data within Webex, such as user profiles and contact lists.
- **Rooms**: These scopes allow you to create, update, and manage rooms within Webex, including adding or removing participants.
- **Messages**: These scopes allow you to send and receive messages within Webex rooms.
- Teams: These scopes allow you to create, update, and manage teams within Webex.
- **Devices**: These scopes allow you to manage Webex devices, including retrieving device details, controlling device features, and managing device settings.
- **Recordings**: These scopes allow you to manage Webex meeting recordings, including retrieving and deleting recordings.
- **Calling**: These scopes allow you to manage Webex calls, provisioning, and reporting.

&nbsp;

### Webex Calling Scopes

To use the Webex Calling APIs, you will need to add one or more of the following scopes for your use case:

#### Calling Provisioning Scopes

These scopes encompass all types of Webex Calling provisioning that an administrator may require.

- `spark-admin:devices_read` - This scope allows you to read the details of Webex Calling devices.
- `spark-admin:devices_write` - This scope allows you to modify the details of Webex Calling devices.
- `spark-admin:organizations_read` - This scope allows you to read the details of organizations associated with Webex Calling.
- `spark-admin:organizations_write` - This scope allows you to modify the details of organizations associated with Webex Calling.
- `spark-admin:people_read` - This scope allows you to read the details of people associated with Webex Calling.
- `spark-admin:people_write` - This scope allows you to modify the details of people associated with Webex Calling.
- `spark-admin:places_read` - This scope allows you to read the details of places associated with Webex Calling.
- `spark-admin:telephony_config_read` - This scope allows you to read Webex Calling settings for a specific organization.
- `spark-admin:telephony_config_write` - This scope allows you to modify Webex Calling settings for a specific organization.
- `spark-admin:workspaces_read` - This scope allows you to read Webex Calling settings for a specific workspace within the organization.
- `spark-admin:workspaces_write` - This scope allows you to modify Webex Calling settings for a specific workspace within the organization.

#### Calling Controls Scopes

These scopes give access to perform actions on an individual's calls.

- `spark:calls_read` – This scope allows you to get call data, including voicemail and call details
- `spark:calls_write` – This scope allows you to control Webex calls like “dial” and “answer”

#### Calling Reporting and Analytics Scopes

These scopes allow reports to be created and run against Webex Calling data.

- `spark-admin:calling_cdr_read` - This scope allows you to retrieve detailed call history information.
- `analytics:read_all` - This scope allows you to 

These scopes should help guide you with your Webex Calling integration.



> **Info**
>
> Depending on your specific use case, you may need additional scopes to fully utilize the Webex Calling APIs.



#### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity)!
