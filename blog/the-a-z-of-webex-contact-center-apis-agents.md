---
type: Article
title: 'The A-Z of Webex Contact Center APIs: Agents'
canonical_url: https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-agents
content_type: blog
date: '2024-11-08'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-agents)

Welcome to the second installment of our blog series, “[The A-Z of Webex Contact Center APIs](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-address-book)”. In this series we are covering the entirety of the RESTful APIs available for the Webex Contact Center, providing insights into their execution and impact from a user's perspective. In this edition we will be going over the [Agents APIs](https://developer.webex.com/webex-contact-center/docs/api/v1/agents), Webhooks, and the use cases that drive their engagement by Webex Contact Center developers.

### Webex Contact Center Agents

An agent is a person who works in a contact center and serves as an interface between customers and businesses. Agents are the most frequent human contact a customer has with a business for solving problems, placing orders, or answering questions about related products and services. Agents can interact with customers using the Webex Contact Center via various channels like voice, instant messaging, Facebook Messenger, WhatsApp, SMS, Email, and more.

Agents utilize many tools while being effective at managing customer inquiries. These tools include CRM (Customer Relationship Management) software, help desk software, SMS management tools, telephones, soft phones, computers, wallboards, predictive dialers and customer satisfaction surveys. Though the Webex Contact Center Agent Desktop consolidates many of these tools into one place, developers are encouraged to use the available developer toolsets to enhance the agent experience.

### The Agent Desktop

The Webex Contact Center Agent Desktop is where agents receive and manage interactions with business customers. They can handle tasks like calls, chats, emails, and more all from one interface in the browser. Agents can access the Desktop and assist customers remotely if they have access to a browser and credentials for their Webex agent user account. They have access to many of the tools mentioned above in the form of custom widgets or out of the box set setup.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf8613a8e1ee71a38/the-a-z-of-webex-contact-center-apis---agents-2.png)

### Custom Agent Desktop with Webex Contact Center RESTful APIs

Third-party developers have been successful at using the available Webex Contact Center RESTful APIs to build custom desktop experiences and CTI (Computer Telephony Integration) connectors that work in a CRM or support tools. For example, [Consilium's UniAgent for Zendesk](https://apphub.webex.com/applications/consilium-uniagent-for-zendesk-crm-consilium-software) solution allows Webex Contact Center Agents to use the Webex Contact Center agent desktop functionality with a custom version of the desktop embedded in Zendesk. This is done through a combination of a [custom headless widget](https://developer.webex.com/blog/unlocking-the-power-of-custom-widgets-in-webex-contact-center) and Webex Contact Center [integration](https://developer.webex.com/docs/integrations).

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt73551e3c59d2d7a6/the-a-z-of-webex-contact-center-apis---agents-3.png)

A subset of the Agents APIs can be used to develop these kinds of integrations, and below we will be going over them and how to get started building custom solutions.

### The Agents REST APIs

Above, an agent is described as a person that works in a contact center. In the context of the APIs, the Agent resource encapsulates the entities that handles [Tasks](https://developer.webex.com/webex-contact-center/docs/api/v1/tasks-call-control) through interactions with customers. Webex Contact Center Administrators and Supervisors can also carry the role of an Agent and trigger the Agents APIs. Agents can be humans or bots operating via the APIs.

#### Get Agent Activities

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities)

The [Get Agent Activities API](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-activities) can be used to get all Agent activities created after a given timestamp epoch. The API returns JSON objects sorted by start time and can be filtered by agent id, team id, and channel type. This API can be used in a reporting tool or confirm findings in a reporting tool. It requires an administrators access token and the scope `cjp:config_read`.

#### Buddy Agent List

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/buddy-agents-list](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/buddy-agents-list)

The [Buddy Agent List API](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/buddy-agents-list) produces a list of agents in a given state and media according to an agent profile setting. In the agent desktop the agent can request a consult or transfer a customer to an available agent based on status. Developers can mimic that behavior using this API and allow agents to set values in a custom input for the media type (Telephony, chat, social, email) or state (Available, Idle) parameters in the API call's request body before producing a list of available agents to transfer or consult with.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte7d0a262a9d22539/the-a-z-of-webex-contact-center-apis---agents-4.jpeg)

#### Login

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/login](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/login)

The [Login API](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/login) is used to log an agent into the Webex cloud. The Login process makes an agent active and visible to administrators and supervisors who use tools like Analyzer and the Supervisor Desktop to monitor how many agents are online and available to assist customers. This process is not to be confused with the OAuth 2.0 flow that is required for users to authorize integrations in the previously mentioned custom desktop integrations.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt563596fca6e8ee5f/the-a-z-of-webex-contact-center-apis---agents-5.png)

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte7c28a6c3aad1a2b/the-a-z-of-webex-contact-center-apis---agents-6.png)

You can see from the above photo of the supervisor agent view (see the agent view below) that after the agent authenticates via Webex, they have included the role, dial number/extension, and team which map to parameters that are included in this APIs request body.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt424532011cbd0d66/the-a-z-of-webex-contact-center-apis---agents-7.png)

#### Logout

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/logout](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/logout)

Logout is the programmatic inverse of login. We are telling the Webex cloud that we are disconnecting and that as an agent, we are no longer available to assist customers. This option is also available when clicking on the icon in the top right corner of the cloud-based Webex Contact Center agent desktop application. The API does require a logout reason in the request body.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8a11674e17b29502/the-a-z-of-webex-contact-center-apis---agents-8.png)

#### Reload

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/reload](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/reload)

When developers are building custom desktops, we have to think about times where we lose network connectivity. This API helps agents re-establish the lost connection to the Webex Cloud session/agent desktop without having to go through the login process to establish a new connection.

#### State Change

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/state-change](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/state-change)

This API allows the user to toggle between states (Available, Idle). The request body requires a State (Available or Idle) which can be provided via an input from the user, and an Auxiliary Code which can be obtained by listing out the [Auxiliary Codes](https://developer.webex.com/webex-contact-center/docs/api/v1/auxiliary-code/list-auxiliary-codes) from the API.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbf20eff78c776a70/the-a-z-of-webex-contact-center-apis---agents-9.png)

#### Get Agent Statistics

[https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-statistics](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/get-agent-statistics)

This API is going to give stake holder several stats on agents in a given time period. Administrators and Supervisors are going to know answers to questions like how many customers an agent handled, how many customers were offered to an agent, how many of those customers were rejected by an agent, how many times did an agent transfer a customer, etc. This is a good API for reporting tools.

### Webhooks

The Agents API also has associated Webhook events. The events are triggered by Agent Login, Agent Logout, and Agent State Change. The Webhooks require `cjp:config, cjp:config_read`.

#### WebSocket Option

Your application can receive notifications during operations like Agent Login, Agent Logout, and Agent State Change by registering a bi-directional WebSocket Connection with the [Subscribe Notification API](https://developer.webex.com/webex-contact-center/docs/api/v1/notification/subscribe-notification). This API can be used with an integration that is scoped for `cjp:user`.

This information is important in the context of this API. When developing a custom desktop, if a developer wants to include webhooks, the Agent State Change API, and necessary Auxiliary Codes API, they will need to include an onboarding step that allows an administrator with permissions to read configurations to authorize the application through the OAuth 2.0 flow for setup. Alternatively, the developer can use the Agent State Change API, or Webhooks, and set up a WebSocket connection with an Agent token. See this sample [starter code](https://github.com/WebexSamples/webex-contact-center-agent-desktop-api-sample) with values hard coded. Developers can choose the path forward given the above information.

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
