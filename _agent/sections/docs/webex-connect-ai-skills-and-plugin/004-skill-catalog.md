---
type: Excerpt
canonical_url: https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Complete the task
- Skill catalog
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/webex-connect-ai-skills-and-plugin). [Full Markdown](../../../../docs/webex-connect-ai-skills-and-plugin.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Before you begin](002-before-you-begin.md) [MCP endpoints, region, and authentication](009-mcp-endpoints-region-and-authentication.md)

## Article introduction

Install and use Webex Connect AI Skills with Codex, Claude Code, Cursor, or standalone skill packages. This guide explains the 19 available skills, plugin and skill installation, tenant and credential prerequisites, common workflows, MCP setup, and production safeguards.

## Parent context

## Complete the task

## Selected section

### Skill catalog

Use the message router for an outbound send request. It selects one channel-specific skill and adds setup, Contact Policy, webhook, or Sandbox guidance when the task requires it.

| Skill | What it does |
| --- | --- |
| [`webex-connect-setup`](https://github.com/webex/webex-skills/blob/main/skills/webex-connect-setup/skill/webex-connect-setup/SKILL.md) | Selects Sandbox or Production, confirms tenant region and API hosts, prepares local configuration, collects required credentials, and configures the supported Production SMS or Email MCP endpoint. SDK and widget builders do not require this API setup. |
| [`webexconnect-android-push-inapp-messaging-builder`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-android-push-inapp-messaging-builder/skill/webexconnect-android-push-inapp-messaging-builder/SKILL.md) | Builds or repairs native Android applications using Webex Connect Push Notifications or In-App Messaging, including registration, chat, notifications, and QA. |
| [`webexconnect-apple-messages-for-business-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-apple-messages-for-business-sendmessage/skill/webexconnect-apple-messages-for-business-sendmessage/SKILL.md) | Builds and validates Apple Messages for Business API v1 text and rich messages, attachments, callbacks, and delivery handling. |
| [`webexconnect-contact-policy`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-contact-policy/skill/webexconnect-contact-policy/SKILL.md) | Uses Contact Policy APIs to manage consent, opt-in and opt-out, channel checks, frequency caps, and send-policy enforcement. |
| [`webexconnect-digital-asset-creation`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-digital-asset-creation/skill/webexconnect-digital-asset-creation/SKILL.md) | Creates, retrieves, and updates Chat, Email, Facebook Messenger, or WhatsApp assets using the selected operation schema and tenant region. |
| [`webexconnect-email-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-email-sendmessage/skill/webexconnect-email-sendmessage/SKILL.md) | Builds, validates, or sends Email with Send Message API v2 or configured Email MCP, including sender discovery, content, callbacks, and receipts. |
| [`webexconnect-facebook-messenger-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-facebook-messenger-sendmessage/skill/webexconnect-facebook-messenger-sendmessage/SKILL.md) | Builds and validates Facebook Messenger API v1 messages for Page-scoped recipients, text, attachments, interactive replies, and callbacks. |
| [`webexconnect-ios-push-inapp-messaging-builder`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-ios-push-inapp-messaging-builder/skill/webexconnect-ios-push-inapp-messaging-builder/SKILL.md) | Builds or repairs native iOS applications using Webex Connect Push Notifications or In-App Messaging, including registration, chat, notifications, and QA. |
| [`webexconnect-livechat-inapp-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-livechat-inapp-sendmessage/skill/webexconnect-livechat-inapp-sendmessage/SKILL.md) | Builds and validates Live Chat and In-App Messaging API v1 requests for messages, threads, attachments, quick replies, notifications, and callbacks. |
| [`webexconnect-livechat-widget`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-livechat-widget/skill/webexconnect-livechat-widget/SKILL.md) | Builds or troubleshoots browser Live Chat widgets using the Webex Connect JavaScript SDK, including registration, threads, messaging, and events. |
| [`webexconnect-mms-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-mms-sendmessage/skill/webexconnect-mms-sendmessage/SKILL.md) | Builds and validates Send Message API v2 MMS requests with media, fallback text, receipts, and callbacks. |
| [`webexconnect-push-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-push-sendmessage/skill/webexconnect-push-sendmessage/SKILL.md) | Builds and validates Push Messaging API v1 requests for registered users or devices, platform payloads, notifications, and callbacks. |
| [`webexconnect-rcs-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-rcs-sendmessage/skill/webexconnect-rcs-sendmessage/SKILL.md) | Builds and validates Send Message API v2 RCS requests, including capability checks, rich content, templates, and SMS fallback. |
| [`webexconnect-sandbox`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sandbox/skill/webexconnect-sandbox/SKILL.md) | Plans supported Sandbox SMS, Voice, and WhatsApp API tests with verified recipients and Sandbox-specific limits. It does not configure Production MCP. |
| [`webexconnect-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sendmessage/skill/webexconnect-sendmessage/SKILL.md) | Routes an outbound request to the right channel skill and adds shared setup, Contact Policy, webhook, or Sandbox guidance when needed. |
| [`webexconnect-sms-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-sms-sendmessage/skill/webexconnect-sms-sendmessage/SKILL.md) | Builds, validates, or sends SMS with Send Message API v2 or configured SMS MCP, including sender discovery, recipients, scheduling, receipts, and callbacks. |
| [`webexconnect-voice-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-voice-sendmessage/skill/webexconnect-voice-sendmessage/SKILL.md) | Builds and validates Voice API v1 and documented Send Message API v2 voice requests for outbound calls, text-to-speech, media, callbacks, and call status. |
| [`webexconnect-webhooks-events`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-webhooks-events/skill/webexconnect-webhooks-events/SKILL.md) | Builds and troubleshoots webhook receivers, callback verification, inbound events, Event API requests, retries, and data streams. |
| [`webexconnect-whatsapp-sendmessage`](https://github.com/webex/webex-skills/blob/main/skills/webexconnect-whatsapp-sendmessage/skill/webexconnect-whatsapp-sendmessage/SKILL.md) | Builds and validates WhatsApp API v1 session replies, approved templates, media, interactive content, and callbacks. |
