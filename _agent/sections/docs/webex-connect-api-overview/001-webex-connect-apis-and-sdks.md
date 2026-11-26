---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-api-overview
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Webex Connect APIs and SDKs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-api-overview). [Full Markdown](../../../../docs/webex-connect-api-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Webex Connect APIs and SDKs

Webex Connect is an Enterprise CPaaS platform that enables you to seamlessly add rich communication capabilities into your existing applications and systems with ease. We offer a robust set of APIs, SDKs, and Webhooks to enable two-way communications across multiple channels, including SMS, Voice, RCS, Apple Messages for Business, WhatsApp, Email, Push Notifications, Live Chat and more.

Use this page as the directory for Webex Connect developer documentation. Digital asset API guidance and reference are available in the Webex Developer Portal. The links for other API families open the existing Webex Connect API documentation.

Webex Connect APIs can be broadly divided into configuration APIs and Messaging APIs. Configuration APIs support capabilities such as digital asset onboarding, channel management, enterprise controls, and integration setup. Messaging APIs support outbound communications across the channels available in Webex Connect.

### Configuration APIs

#### Digital Channel Onboarding APIs

Digital channel onboarding enables you to set up channel assets for Webex services. You can onboard and manage supported digital channel assets through Control Hub or programmatically using Webex Connect APIs.

API-based onboarding uses a Webex personal access token with the required scope. The user represented by the token must have access to the organization and permission to manage channel assets.

See [Digital Channel APIs](https://developer.webex.com/docs/webex-connect-create-your-first-digital-asset) for available operations and schemas.

#### Contact Policy APIs

Contact Policy APIs help you manage customer consent and communication preferences. Use them to group message types, such as statements and reminders, and control how often customers receive each category. The Contact Policy application must be enabled for the Webex Connect organization before these APIs can be used.

See the [Contact Policy APIs](https://developers.webexconnect.io/reference/post_v1-groups-4) in the existing Webex Connect API documentation.

#### Profile APIs

Profile APIs help you create and manage Customer Profiles and Application Profiles. Customer Profiles store customer attributes, channel identifiers, and communication preferences across channels. Application Profiles store customer information associated with a specific communication channel.

See the [Profile API overview](https://developers.webexconnect.io/reference/profile-api-overview).

#### Thread APIs

A thread is used to stitch together all messages sent or received within a particular context into a conversation. Webex Connect offers the ability to create, update, delete, and list threads to enable businesses to make one-way announcements or hold two-way conversations with their Chat (Mobile/Web app) users.

See the [Thread APIs](https://developers.webexconnect.io/reference/overview-of-thread-apis).

#### Events and webhooks

Custom Event APIs and inbound webhooks send application events into Webex Connect. Outbound webhooks deliver events such as delivery receipts and incoming messages from Webex Connect to your application.

See [Outbound Webhooks](https://developers.webexconnect.io/reference/outbound-webhooks-api-ref) and [API Authentication](https://developers.webexconnect.io/reference/api-authentication) in the existing documentation.

#### Webex Connect SDKs

The Webex Connect SDKs simplify the integration of Push Notifications, In-App Messaging, and Live Chat into mobile and web applications. Use the Android, iOS, and JavaScript SDKs to build interactive communication experiences.

See the [Webex Connect SDK overview](https://developers.webexconnect.io/docs/overview-of-sdks).

### Messaging APIs

Webex Connect Messaging APIs help you connect with customers across SMS, MMS, RCS, WhatsApp, Email, Push Notifications, In-App Messaging, Live Chat, and other supported channels. Use them to send simple text alerts or deliver rich, interactive experiences from your applications. The APIs provide the flexibility and scale needed to support a wide range of customer engagement use cases.

Start with the [Messaging API introduction](https://developers.webexconnect.io/reference/getting-started-with-your-messaging-api), then use the channel documentation below.

| Messaging API | Existing API documentation |
|---|---|
| SMS | [SMS APIs](https://developers.webexconnect.io/reference/sms-apis) |
| MMS | [MMS API](https://developers.webexconnect.io/reference/mms-api) |
| RCS | [RCS APIs](https://developers.webexconnect.io/reference/rcs-apis) |
| RCS Capability Lookup | [RCS Capability Lookup API](https://developers.webexconnect.io/reference/capability-api) |
| Number Intelligence Lookup | [Number Intelligence API](https://developers.webexconnect.io/reference/number-intelligence-api) |
| Email | [Email API](https://developers.webexconnect.io/reference/email-api) |
| Push Notifications | [Push API](https://developers.webexconnect.io/reference/push-api) |
| Live Chat and In-App Messaging | [Live Chat and In-App Messaging API](https://developers.webexconnect.io/reference/live-chat-in-app-messaging-api) |
| Apple Messages for Business | [Apple Messages for Business API](https://developers.webexconnect.io/reference/apple-messages-for-business-apis) |
| Messenger | [Facebook Messenger API](https://developers.webexconnect.io/reference/facebook-messenger-api) |
| WhatsApp | [WhatsApp API](https://developers.webexconnect.io/reference/whatsapp-apis) |

Messaging APIs generally acknowledge whether a request was accepted or rejected before the final channel outcome is known. Use the callback and outbound webhook documentation to process delivery receipts, incoming messages, and other events.

#### Voice APIs

Voice APIs provide capabilities for building interactive voice experiences. Use them to initiate outbound voice notifications, design interactive call flows using APIs and webhooks, monitor call status, and retrieve call recording details.

See [Voice APIs](https://developers.webexconnect.io/reference/voice-apis) in the existing API documentation.
