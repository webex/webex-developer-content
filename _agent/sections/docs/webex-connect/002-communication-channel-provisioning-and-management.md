---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Communication channel provisioning and management
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect). [Full Markdown](../../../../docs/webex-connect.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Integration setup and management](003-integration-setup-and-management.md)

## Selected section

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
