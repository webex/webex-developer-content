---
type: Article
title: There is a New Integration Scope in Town!
canonical_url: https://developer.webex.com/blog/there-is-a-new-integration-scope-in-town-
content_type: blog
date: '2017-06-10'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/there-is-a-new-integration-scope-in-town-)

Recently we added a new integration scope called spark:all. The spark:all scope acts as an overall aggregate for the rest of the user scopes. It basically requests full access to a Spark account, i.e. reading/writing messages, creating/deleting spaces, making/receiving calls, and so on.

From an integrations standpoint, this makes it really simple to communicate to a user that the app requires full access without needing to select individual user scopes (such as spark:messages_read, spark:messages_write, spark:people_read). This is particularly useful for heavy-duty integrations, such as Cisco Spark calling apps. Prior to spark:all, individual user scopes were grouped and presented to the user for approval; with spark:all it requires approval for just one 'super' scope.

When spark:all is selected, the rest of the user scopes will be disabled for selection:

![Scopes][1]

Even though spark:all acts as an aggregate scope, it is important to note that in the grant flow, the spark:all scope only aggregates user scopes – admin scopes are not part of spark:all and can be applied as add-ons, but no other user scope should be added when spark:all is selected.

Users will be presented with the following screen in the grant flow when the integration requires spark:all:

![Authorization][2]

The spark:all scope is optional for the majority of the integrations. However, it is required for any app that uses calling features – you're effectively replicating a large portion (if not all) of a native Spark client at that point and need the complete set of scopes in order for your integration to function correctly.

To learn more about integrations, please see the [Authentication guide](https://developer.ciscospark.com/authentication.html).

We focus on providing you the best features and experience. If you have any questions, feel free to reach out to us at [devsupport@ciscospark.com](mailto:devsupport@ciscospark.com) or join the [DevSupport Spark room](https://developer.ciscospark.com/support.html). Follow us on [Twitter](https://twitter.com/ciscosparkdev) to stay updated.

  [1]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt40db04bd85e6b7e3/5b649370f9cd894d3d8accbb/108210_Scopes.png
  [2]: https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdf04d0496d057f45/5b64938e7eac3e673d5e67a6/108211_Authorization.png
