---
type: Article
title: Introducing Service Apps for Webex Contact Center
canonical_url: https://developer.webex.com/blog/introducing-service-apps-for-webex-contact-center
content_type: blog
date: '2025-04-25'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-service-apps-for-webex-contact-center)

We are pleased to announce that [Service Apps](https://developer.webex.com/webex-contact-center/docs/contact-center-service-apps) have been made available for Webex Contact Center. With Service Apps, mission critical Contact Center integrations can now be deployed on behalf of an organization instead of individual users. With a standard integration, if the authorizing user departs or updates their password, the integration will simply stop working. Conversely, a Service App can request data for multiple users throughout an entire organization, rather than just a single user. This provides much more flexibility for tasks that run continually in an organization. Let’s explore some of the most optimal use cases for Service Apps in Contact Center.

#### Service App Use Cases for Contact Center

When Service Apps were [first introduced](https://developer.webex.com/blog/service-apps-revolutionizing-business-apps-for-more-efficient-workflows) to Webex for Developers, they were targeted towards Webex administrator tasks such as automated provisioning, Compliance Officer tasks that poll the Events API, and creating Webex guest accounts. The original Service Apps guide for those application types can be found [here](https://developer.webex.com/docs/service-apps). In Webex Contact Center, Supervisor-level tasks that are needed on a persistent basis are the most prominent use for Service Apps. This can be things like monitoring agent performance, improving customer escalations, and generating analytics for active reporting.

One example would be a Service App for agent call recording, using the [Captures API or Webhooks](https://developer.webex.com/webex-contact-center/docs/api/v1/captures) to retrieve and analyze recorded interactions. This can be for supervisors to ensure quality control and compliance throughout the organization, provide training and feedback to agents, and handle dispute resolutions more effectively. Call recording is certainly an ideal scenario for a Service App since it will need to be active every business day for all agents on duty.

Another great way a Service App can be leveraged in Webex Contact Center is for a reporting system through the [Search API or Webhooks](https://developer.webex.com/webex-contact-center/docs/api/v1/search). Again, this type of app needs to stay active on a long-term basis to extract all the report data for each day. From there, it can send that data to a third-party service such as [Microsoft Power BI](https://www.microsoft.com/en-us/power-platform/products/power-bi) or [Snowflake](https://www.snowflake.com/en/product/analytics/) to create visual representations or populate dashboards with specific metrics. For more information on how to work with this endpoint, check out the [Getting Started with the Search API](https://developer.webex.com/webex-contact-center/docs/getting-started-with-search-api) guide.

#### Developer Workflows for Contact Center Service Apps

Webex Service Apps and traditional integrations do have several similarities, as both are based on the OAuth 2.0 protocol. While the OAuth client creation and scope selection occur for both, the process for obtaining access tokens is different for Service Apps. The process can either be done completely within the GUI interface of the Webex Developer portal or automated via API and webhooks. Regardless of the method, it is first contingent upon administrator authorization in Control Hub to start the process for obtaining the Service App tokens. To start testing this out, make sure to get a free [Contact Center Developer Sandbox](https://developer.webex.com/webex-contact-center/docs/sandbox_cc) that provides administrator access and licenses to your own organization.

The [developer guide](https://developer.webex.com/webex-contact-center/docs/contact-center-service-apps#token-retrieval-via-api) has step-by-step instructions on how to create a Service App for Contact Center and retrieve access &amp; refresh tokens. When creating a new Service App for Contact Center, any of the [integration scopes](https://developer.webex.com/docs/integration-scopes) are valid (depending on the use case), except for `spark:applications_token` and `spark:kms`. These two scopes are still important to Service Apps, as they correspond to the *Access Token API* for automating the token retrieval process. In this scenario, a token retrieval app needs to be created as a *separate* integration from the Service App that will implement the tokens to access the APIs. You can also find more information on retrieving the Service App tokens via API in the [Authentication guide](https://developer.webex.com/docs/authentication).

To see how it all comes together, check out this Node.js [Service App Token Getter](https://github.com/WebexSamples/service_app_token_getter) demo app that incorporates the entire Service App authorization workflow to obtain access and refresh tokens. The app first creates a Node.js server to manage OAuth processes for a Webex Integration and creates webhooks for Service App authorization events. From there, the server listens for HTTP requests and processes them to manage authorization and tokens. You can even run the demo locally on your machine for quick testing.

#### Need Some Help? No Problem!

As always, we are happy to provide developer support for any of the features mentioned here. If you need help or have any questions, the [Webex Developer Support Team](https://developer.webex.com/support) is always eager to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Until next time, happy developing on Webex!
