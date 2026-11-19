---
type: Guide
title: Webex Connect | Overview
display_title: Overview
canonical_url: https://developer.webex.com/docs/webex-connect
content_type: documentation
product_group:
- webex-connect
categories:
- webex-connect
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/webex-connect)

## About Webex Connect

Webex Connect is an easy-to-use cloud communications platform that is secure and scalable, enabling enterprise developers to build smarter interactions and richer, frictionless experiences across communication channels, reducing complexity and enabling rapid innovation.

Webex Connect is a fully programmable CPaaS solution with a choice of APIs, SDKs, and low-code tools. It includes capabilities for full lifecycle management of interactive customer experiences and focuses on six key areas:

1. Communication channel provisioning and management
2. Integration setup and management
3. Business logic and flow orchestration
4. Multichannel messaging
5. NLP, NLU, and AI-powered conversation automation
6. Intelligent enterprise control, monitoring, and reporting

## Communication channel provisioning and management

Communication channels connect Webex Connect to the services that customers use to interact with your organization. Channel assets can represent Email configurations, mobile or web applications, messaging accounts, phone numbers, senders, or channel-specific applications.

### Onboard channel assets

Set up channel assets through any of the supported options for your channel and Webex service:

| Set up through | Use it for | Documentation |
|---|---|---|
| Webex Connect | Configure supported channel assets in the Webex Connect portal. | [SMS](https://help.webexconnect.io/docs/welcome#sms), [RCS](https://help.webexconnect.io/docs/welcome#rcs), and [other supported channels](https://help.webexconnect.io/docs/welcome#channel-support) |
| Control Hub | Create and manage supported channel assets and assign them to a Webex service. | [Configure an Email asset](https://help.webex.com/article/nrelvg3) and [Configure a Chat asset](https://help.webex.com/article/11dtv5) |
| Developer Portal APIs | Programmatically create and manage supported Email and Chat assets. | [Digital asset APIs](https://developer.webex.com/docs/webex-connect-api-overview#digital-channel-onboarding-apis) and [Create Your First Digital Asset](https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset) |

The configuration options available for an asset depend on its channel, assigned Webex service, and setup method.

### Supported communication channels

| Channel | What you can build | Platform documentation |
|---|---|---|
| SMS | Alerts, notifications, two-way messaging, and high-volume campaigns. | [SMS](https://help.webexconnect.io/docs/welcome#sms) |
| RCS | Branded, rich, interactive messages with device-capability checks and SMS fallback. | [RCS](https://help.webexconnect.io/docs/welcome#rcs) |
| Branded Text | Verified and branded messaging that can upgrade eligible SMS traffic to RCS. | [Branded Text](https://help.webexconnect.io/docs/branded-text) |
| WhatsApp | Business-initiated and customer-initiated WhatsApp conversations. | [WhatsApp](https://help.webexconnect.io/docs/whatsapp) |
| Push Notifications | Deliver push notifications to mobile and web applications using Webex Connect SDKs. | [Push Notifications](https://help.webexconnect.io/docs/welcome#push-notifications) |
| Live Chat and In-App Messaging | Build real-time Live Chat and In-App Messaging experiences for mobile and web applications. | [Live Chat and In-App Messaging](https://help.webexconnect.io/docs/welcome#live-chat-and-in-app-messaging) |
| Email | Transactional and journey-based email using configured Email assets. | [Email](https://help.webexconnect.io/docs/welcome#email) |
| Voice | Outbound notifications, programmable calling, interactive voice response, and call recording. | [Voice](https://help.webexconnect.io/docs/welcome#voice) |
| MMS | Multimedia messaging containing images, audio, video, and text. | [MMS](https://help.webexconnect.io/docs/welcome#mms) |
| Apple Messages for Business | Rich customer conversations through Apple Messages for Business. | [Apple Messages for Business](https://help.webexconnect.io/docs/apple-messages-for-business-setup) |
| Messenger | Customer conversations through a connected Facebook Page. | [Messenger](https://help.webexconnect.io/docs/facebook-messenger) |

### Channel management

Templates provide reusable message content for supported channels. Customer and application profiles store customer identifiers, attributes, and communication context. Contact policies help manage consent, preferences, and communication frequency.

See the [Webex Connect platform documentation](https://help.webexconnect.io/docs/welcome) for channel configuration and lifecycle guidance.

### Webex Connect SDKs

The Webex Connect SDKs provide a framework for building rich Live Chat, In-App Messaging, and push notification experiences within mobile and web-based applications.

See the [Webex Connect SDK overview](https://developers.webexconnect.io/docs/overview-of-sdks) for supported platforms, capabilities, and SDK documentation.

## Integration setup and management

Use integrations to exchange events and data between Webex Connect and enterprise systems. Webex Connect supports inbound and outbound webhooks, custom events, custom nodes, authorizations, and pre-built integrations.

| Capability | Use it for | Documentation |
|---|---|---|
| Inbound webhooks | Notify Webex Connect about events in an external application and trigger flows or rules. | [Inbound Webhooks](https://help.webexconnect.io/docs/inbound-webhooks) |
| Outbound webhooks | Deliver events such as delivery receipts and incoming messages from Webex Connect to an application. | [Outbound Webhooks](https://help.webexconnect.io/docs/outbound-webhooks) |
| Custom events | Send business events and associated data to Webex Connect to trigger flows or rules. | [Custom Events](https://help.webexconnect.io/docs/custom-events) |
| Custom nodes | Create reusable REST or SOAP integrations for use in flows. | [Custom Node Integration](https://help.webexconnect.io/docs/custom-nodes-integration) |
| Authorizations | Configure credentials used by services, APIs, inbound webhooks, and integration nodes. | [Service Key and JWT Authentication Tokens](https://help.webexconnect.io/docs/service-key-and-jwt-authentication-tokens) |
| Pre-built integrations | Connect flows to supported CRM, contact center, bot, healthcare, and customer-data systems. | [Pre-built Integrations](https://help.webexconnect.io/docs/pre-built-integrations-introduction) |

## Business logic and flow orchestration

Use services, flows, and rules to organize and automate customer journeys. A service provides a workspace for related assets, integrations, credentials, flows, and rules.

| Capability | Use it for | Documentation |
|---|---|---|
| Services | Organize the components and credentials associated with a customer interaction use case. | [What's a Service](https://help.webexconnect.io/docs/service-introduction) |
| Flow Builder | Design, test, publish, and manage multi-step customer interaction flows. | [Flows](https://help.webexconnect.io/docs/flows-introduction) |
| Rules | Automate simpler tasks using triggers, conditions, and actions. | [Rules](https://help.webexconnect.io/docs/rules) |

## Multichannel messaging

Use Webex Connect to send and receive communications across SMS, MMS, RCS, Email, Push Notifications, Live Chat, In-App Messaging, Apple Messages for Business, Messenger, WhatsApp, and other supported channels. Applications can send messages through APIs or orchestrated flows and receive delivery receipts, incoming messages, and other events through webhooks.

See the [Webex Connect API Overview](https://developer.webex.com/docs/webex-connect-api-overview#messaging-apis) to find the available Messaging API documentation. For API families that remain in the existing documentation, see the [Messaging API introduction](https://developers.webexconnect.io/reference/getting-started-with-your-messaging-api).

## NLP, NLU, and AI-powered conversation automation

Use AI agents and conversational automation to understand customer requests, generate responses, perform actions, and hand interactions to other systems or human agents when required.

| Capability | Documentation |
|---|---|
| Create and manage AI agents | [Getting Started with Webex AI Agent Studio](https://help.webexconnect.io/docs/getting-started-with-webex-ai-agent-studio) |
| Connect AI agent actions to Webex Connect flows | [Configure Fulfillment Flows for AI Agent Actions](https://help.webexconnect.io/docs/configure-fulfilment-flows-for-ai-agent-actions) |

## Intelligent enterprise control, monitoring, and reporting

Use enterprise controls to organize access, assign roles, manage organizational hierarchies, apply contact policies, audit administrative activity, and monitor platform and interaction performance.

| Capability | Documentation |
|---|---|
| User roles and role-based access control | [User Roles](https://help.webexconnect.io/docs/user-roles-and-hierarchy) |
| Groups and teams | [Groups and Teams](https://help.webexconnect.io/docs/getting-started-groups-and-teams) |
| Administrative audit activity | [User Audit](https://help.webexconnect.io/docs/user-audit) |
| Customer consent, preferences, and communication frequency | [Contact Policy](https://help.webexconnect.io/docs/contact-policy) |
| Messaging, voice, and flow reporting | [Reports](https://help.webexconnect.io/docs/service-reports) |
| Transaction and execution diagnostics | [Debug Console](https://help.webexconnect.io/docs/console) |
| Platform updates | [Platform changelog](https://help.webexconnect.io/changelog) |

## Next steps

- Review the [Webex Connect API Overview](https://developer.webex.com/docs/webex-connect-api-overview).
