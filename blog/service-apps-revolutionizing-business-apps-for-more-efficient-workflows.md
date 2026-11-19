---
type: Article
title: 'Service Apps: Revolutionizing Business Apps for More Efficient Workflows'
canonical_url: https://developer.webex.com/blog/service-apps-revolutionizing-business-apps-for-more-efficient-workflows
content_type: blog
date: '2023-04-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/service-apps-revolutionizing-business-apps-for-more-efficient-workflows)

Business apps don't have to be dull, especially with the introduction of Service Apps to the Webex family. These new apps are changing the game by providing a highly efficient way to simplify your admininstrator’s workday and streamline your automation systems. By utilizing the power of bots combined with the security of integrations and the inherent reliability of the OAuth 2.0 industry standard, Service Apps are a must-have for your most critical business flows.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb7417c85d7322102/644ac80bdf452f0942b2d8ee/one.png)

### What are Service Apps?

If you're wondering what Service Apps are, they are an exciting new type of application available in the [Webex developer program](https://developer.webex.com/). These apps have been specifically designed to tightly integrate your most sensitive and guarded business flows to Webex, without worrying about the security and integrity of your data, even if a user changes their password or leaves the company. Service Apps work seamlessly with the existing concepts of bots and integrations you're already familiar with, and if you're not, we have [amazing tutorials](https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration) to help you get started.

### Taking a Closer Look

Let's take a closer look at some of the key features of Service Apps. First, they can be used anywhere you would use an admin-authorized integration. Think of them as virtual administrators that can help automate the provisioning and licensing of users, generate quality and usage reports, perform diagnostics and troubleshooting, and more. Service Provider admins do these same tasks but on a much larger scale, so automation tools are necessary to make these admins more nimble, agile, and effective. Service Apps can power these automation tools by creating a machine account in the org that makes the Webex API calls. This machine account has the role of a full admin with the assigned scopes, and since it doesn't show in any user lists, it can't be accidentally deleted or subject to password changes, making it highly secure and independent from human error. Of course, admins can decommission the machine account by deauthorizing the Service App in Control Hub. Both authorization and deauthorization must be done deliberately and leave an audit trail in Control Hub.

### Calling the APIs with a Service App

As a result of the Service App's creation and authorization flow, the familiar access and refresh tokens are produced, which are used to access the Webex APIs, just like with integrations. In fact, existing Integrations can be upgraded to Service Apps by simply switching the tokens. In the meetings REST APIs, we have many endpoints that allow an admin to act on behalf of any user provisioned on the site. Service Apps can take on this task. What they cannot do, though, is act on resources that require a meetings license like hosting a meeting.

### A Service App Example

Take, for example, scheduling meetings on behalf of Jennifer, Jeff, and Jill, as indicated by their email addresses. Those are perfect candidates for Service Apps. The Service App can be used with the admin on-behalf REST calls for tight integration to a proprietary calendaring system. Clearly, this system should never stop, since your users rely on it. And you want any of your admins to be able to manage such a mission-critical system.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt82808edca1421004/644ac81d25dc1411156001db/two.png)

**NOTE**: It's important to understand that Service Apps have some limitations, such as the inability to use XSI scopes or query CDR records. However, the development team is filling these gaps on an as-needed basis, so feel free to [make an AHA request](https://ciscocollaboration.ideas.aha.io/).

### Perfect for Mission Critical, Long-standing Processes

In summary, Service Apps are best for mission-critical, long-standing processes you don't want to tie to a user but feel comfortable letting a virtual admin handle independently. They are ideal for tying your business apps tightly to Webex, collecting and aggregating data on an org-wide basis, creating a virtual admin that powers your automation tools, and acting on behalf of users in meetings APIs.

### Where to go Next

If you're interested in Service Apps, we've developed some nice GUI flows for them, including a Control Hub view and a Developer Portal view. Check out our [guide](https://developer.webex.com/docs/service-apps) to start experimenting with them, which takes just a few minutes until you have your tokens in hand. As always, you can also reach out to our [Dev Support Team](https://developer.webex.com/support) if you have any questions.

Don't get left behind - join the Service App revolution today and experience the ultimate in workplace efficiency!
