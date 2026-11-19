---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-contact-center-web-sdk-quickstart). [Full Markdown](../../../../../docs/sdks/webex-contact-center-web-sdk-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Welcome to the Quick Start Guide for the Webex Contact Center (WxCC) SDK.

---

This guide is designed to help developers quickly set up, authenticate, and interact with the WxCC SDK. By following this guide and integrating the provided code snippets, you'll be able to log in an agent, manage agent states, and handle incoming tasks efficiently. Let's get started!

## Selected section

## Troubleshooting

The Webex Contact Center SDK provides methods to upload logs for diagnosing and resolving issues. These logs include actions taken on the SDK such as login, logout and call handling, which can help Webex support troubleshoot SDK-related problems. The logs also include tracking and feedback IDs that can be shared with developer support to download the required logs remotely.

### Upload Logs

The `uploadLogs` method allows you to manually upload logs at any point during SDK usage. This is particularly useful when you encounter unexpected behavior or need to provide diagnostic information to Webex support.

#### Example Usage

```js
const uploadLogsResponse = await webex.cc.uploadLogs({ description: 'Optional issue description' });
// uploadLogsResponse.feedbackID contains the ID for the uploaded logs.
```

In addition to manual uploads, the SDK can automatically upload logs when certain errors occur. This ensures that critical diagnostic information is captured without requiring manual intervention. 

To expedite issue resolution, provide the following details to Webex support:

- **Correlation ID** or **feedbackID from the console logs/network requests** or 
- **User ID** with **Timestamp** of the error

These details help Webex support quickly locate the relevant logs and resolve the issue efficiently.

#### When to Use

- **Manual Uploads**: Use when you want to capture logs at a specific point in your application workflow.
- **Auto Uploads**: Logs are automatically uploaded during unexpected errors or failures. Users only need to provide the **Correlation ID**, **feedbackID** from console logs or network request/responses, or **User ID** with a **Timestamp** to Webex support for faster issue resolution.

By leveraging both manual and automatic log uploads, you can ensure comprehensive diagnostics and faster issue resolution.
