---
type: Article
title: Introducing the Webex Contact Center APIs and Developer Portal
canonical_url: https://developer.webex.com/blog/introducing-the-webex-contact-center-apis-and-developer-portal
content_type: blog
date: '2023-04-25'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/introducing-the-webex-contact-center-apis-and-developer-portal)

The Webex Contact Center suite is a “pure-cloud” solution that solves Contact Center business problems and helps run efficient customer experience centers to maximize customer satisfaction and transform “Contact centers” into “Experience centers”.

The Contact Center application suite enables omnichannel inbound interaction routing, (Voice, Chat, Email, Social, SMS, and more) and helps business connect their customers to agents by passing customer context with a data-driven routing model – bringing in customer interactions on an Agent Desktop application where users can manage these interactions effectively. The Webex Contact Center APIs surface the power of the platform by providing all the interfaces used by in-house applications and makes them available publicly to developers on the Developer Portal.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9500efa219cd330a/6448069388e91a10e63c9942/Picture1.png)

The platform now has a powerful set of APIs that serve all these use cases and can be grouped into the following groups. We will trace the entire life cycle of a Contact Center interaction and understand how these maps to the APIs available on the Developer Portal.

### Authentication

Webex Contact Center API Authentication works on the OAuth2 specification outlined in [API Authentication](https://developer.webex.com/docs/authentication) and requires the application to secure a temporary Access Token to access the APIs.

This token is secure and expires after a certain duration. To learn more about Authentication, see the [Authentication Sample](https://github.com/CiscoDevNet/webex-contact-center-api-samples/tree/main/app-auth-sample).

#### Can an application secure permanent access to the APIs without user intervention?

Learn about token management and the Refresh Token flow for apps that do not require user logins. [The Token Management Sample](https://github.com/CiscoDevNet/webex-contact-center-api-samples/tree/main/token-app-sample) shows you how to get an access token that refreshes in the background to maintain API access with Webex Contact Center.

### Provision a Contact Center using Configuration APIs

![Contact Center Settings on Admin Portal](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt107aba4b16552918/6434616a8485c010da11a81f/contact-center-intro-4.png)



> **Info**
>
> The admin settings are now available in the Contact Center Admin Portal but those controls will be migrated to Webex Control Hub shortly.



Before you begin using the APIs it is important to understand the flow of a contact through the system. First, a contact hits an Entry Point which is mapped to a Flow orchestration script that chooses the contact handling, along with the Queue that is chosen to pick an Agent from a given Team of Agents. These APIs are configured for users with an “admin” scope.

The configuration APIs available today - Create, Read, Update, and Delete (CRUD) endpoints via REST APIs, make this end-to-end configuration possible via touchless automation.

Some key admin controls include:

- Entry Points ([https://developer.webex.com/webex-contact-center/docs/api/v1/entry-point](https://developer.webex.com/webex-contact-center/docs/api/v1/entry-point))
- Queues ([https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues))
- Teams ([https://developer.webex.com/webex-contact-center/docs/api/v1/team](https://developer.webex.com/webex-contact-center/docs/api/v1/team))
- Users ([https://developer.webex.com/webex-contact-center/docs/api/v1/users](https://developer.webex.com/webex-contact-center/docs/api/v1/users))
- User Profiles ([https://developer.webex.com/webex-contact-center/docs/api/v1/user-profiles](https://developer.webex.com/webex-contact-center/docs/api/v1/user-profiles))
- Agent Profiles ([https://developer.webex.com/webex-contact-center/docs/api/v1/user-profiles](https://developer.webex.com/webex-contact-center/docs/api/v1/user-profiles))
- Address Books ([https://developer.webex.com/webex-contact-center/docs/api/v1/address-book](https://developer.webex.com/webex-contact-center/docs/api/v1/address-book))
- Idle codes ([https://developer.webex.com/webex-contact-center/docs/api/v1/auxiliary-code](https://developer.webex.com/webex-contact-center/docs/api/v1/auxiliary-code))

And many more.

Learn more on how to build a configuration management application powered by these configuration APIs using our samples below:

- [Configuration Automation Sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/configuration-samples/configuration-app-sample)
- [Configuration Extraction Sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/configuration-samples/configuration-extraction-sample)

&nbsp;

### Reporting and Recording APIs

No Contact Center is complete without compliance recording and reporting and analytics. The Call Recording API (Captures API) allows you to retrieve call recordings securely from the platform for post-call analytics.

The reporting APIs on Webex Contact Center allow a developer to extract Contact Center reporting data. The reporting APIs today have 3 flavors of interfaces that can be leveraged to build a full-fledged reporting capability that supplements the Webex Contact Center solution.

![Sample records for key contact center personas](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltae83702b32e5451c/6434616a50e4c910ff3973bf/contact-center-intro-5.png)

#### Webhooks for Contact Center reporting

Webhooks form a great system for working with near-real-time data, and for reacting to Contact Center events using custom logic. If you want to stay on top of a busy contact center or have an application that can’t wait for slow batch reports or expensive API polling-and-diffing solutions, webhooks are the way to go:

- Real-time webhooks ([https://developer.webex.com/webex-contact-center/docs/api/v1/captures](https://developer.webex.com/webex-contact-center/docs/api/v1/captures))
- Tasks Webhooks ([https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control))
- Agent Webhooks ([https://developer.webex.com/webex-contact-center/docs/api/v1/agents](https://developer.webex.com/webex-contact-center/docs/api/v1/agents))

&nbsp;

#### GraphQL Powered REST API

The [Search API](https://developer.webex.com/webex-contact-center/docs/api/v1/search) is a GraphQL (Graph Query Language) powered REST API that provides access to both historical and real-time raw data feeds. The API is called using and supports all the fields that are used by Webex Contact Center Analyzer reporting to store contact center data on the platform.

Look at our samples to learn more about how you can use our GraphQL API:

- Get started with GraphQL, see the GraphQL Sample ([https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-sample))
- To learn how GraphQL can be used to extract data used by a 3rd party solution, see the GraphQL PowerBI Sample ([https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-powerbi-sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-powerbi-sample))

&nbsp;

#### REST APIs for Reporting

The following APIs provide interfaces with a stock set of fields to extract reporting data:

- Queue Statistics API ([https://developer.webex.com/webex-contact-center/docs/api/v1/queue-statistics](https://developer.webex.com/webex-contact-center/docs/api/v1/queue-statistics))
- Agent Statistics API ([https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-statistics](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-statistics))
- Agent Activities API ([https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities))

To learn how these Reporting APIs can be used to extract data into a 3rd party Reporting Wallboard solution, see [Wallboard Sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/reporting-samples/graphql-wallboard-sample).

### Create Agent and Supervisor Tools using Desktop APIs

The Contact Center Desktop for Agents and Supervisors is the application used to service contact center interactions. Although Webex Contact Center provides a fully loaded Agent and Supervisor Desktop, the Developer Portal surfaces all the APIs and technologies used to power this desktop.

![A screenshot of Agent Desktop and all the tools available at their disposal while performing contact center-related tasks](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt31d7fc53b23ffd52/6434616acbf47d113c0b217a/contact-center-intro-6.png)

The configuration APIs described above provide a way to list configurations on the desktop, such as Agent Profiles, Users, Idle Codes, Wrap up Codes, Address Books, and other settings used by an Agent or Supervisor.

Along with these, we provide a full set of Desktop APIs – both in REST and Websocket flavors bringing in the ability to build a fully integrated, 3rd party event-based desktop application.

The main APIs for an Agent function include:

- Login
- State Change

And the main APIs for Call control, are covered by the Call Control APIs:

- Accept
- End
- Transfer
- Conference
- Pause
- Resume

And all these APIs can be found on the [Agents Page](https://developer.webex.com/webex-contact-center/docs/api/v1/agents).

This is supplemented by a full set of WebSocket notifications that can be subscribed to by using the [Notification API](https://developer.webex.com/webex-contact-center/docs/api/v1/notification).

- For a full set of web socket notification payloads, see the [Contact Control APIs guide](https://developer.webex.com/webex-contact-center/docs/contact-control-apis).
- Build a custom desktop using the Desktop APIs, see the [Desktop API sample](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/desktop-sample/desktop-api-sample).

&nbsp;

### What Next?

We’re excited to see what you are going to build. To get started visit the [Webex Contact Center Developer’s Portal](https://developer.webex.com/webex-contact-center/docs). We also have a great [support team](https://developer.webex.com/support) to help you out!
