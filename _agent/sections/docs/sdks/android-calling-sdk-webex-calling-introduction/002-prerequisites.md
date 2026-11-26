---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-introduction
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Prerequisites
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-webex-calling-introduction). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-webex-calling-introduction.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [License Requirements](001-license-requirements.md)

## Article introduction

Webex Calling, a cloud-based phone system from Webex by Cisco, allows users to make and receive calls.

---

As of version 3.9.1, Android developers can now incorporate Webex calling capabilities into their own applications.

## Selected section

## Prerequisites

Make sure you meet the following prerequisites before using the SDK Webex calling features:

* Register an app in the Developer Portal as described in the following [link](https://developer.webex.com/docs/sdks/register-your-app).
* Follow the steps to integrate the SDK into your Android app as described in the following [link](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk).
* For Webex Mobile SDK initialization and OAuth-based login configuration, refer to the first example in this [link](https://developer.webex.com/docs/sdks/android-calling-sdk-authorization).
* Incoming Webex Calling notifications are sent via webhooks to SDK-integrated mobile apps. The admin can set up a [firehose webhook](https://developer.webex.com/docs/webhooks#the-firehose-webhook) targeting `telephony_push` events. Upon receiving a webhook payload, it should be processed and forwarded from the backend server to the mobile app via APNS or FCM for handling.
