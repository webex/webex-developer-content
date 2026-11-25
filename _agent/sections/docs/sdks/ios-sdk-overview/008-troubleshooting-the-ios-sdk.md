---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-sdk-overview
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting the iOS SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-sdk-overview). [Full Markdown](../../../../../docs/sdks/ios-sdk-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](005-requirements.md)

## Article introduction

Build iOS apps with the **Webex iOS SDK**. Find supported features, requirements, samples, and API references.

## Selected section

## Troubleshooting the iOS SDK

If you're having trouble with the iOS SDK, here's some more information
to help troubleshoot the issue.

### Additional Logging

You can enable additional logging to your application to help narrow down any issues with the SDK.

#### Enabling console logging

```swift
webex.enableConsoleLogger = true
webex.logLevel = .verbose
```

### Upload Diagnostic Logs

The SDK supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. The uploaded bundle contains the same SDK diagnostic logs and media engine logs that are available through the existing `webex.getLogFileUrl()` API. For full details including response handling and error codes, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-ios-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

### Firewall Ports

The iOS SDK makes use of the following network ports. If you're encountering connection issues, make sure there aren't any firewalls blocking or preventing communication over these ports:



| Service       | Protocol              | Port(s)                                       |
| ------------- | --------------------- | --------------------------------------------- |
| Messaging     | HTTPS                 | 443                                           |
| Notifications | WebSocket             | 443                                           |
| Calls         | HTTPS                 | 443                                           |
| Media         | RTP/SRTP over UDP/TCP | 33434-33598, 8000-8100 or 33434 (shared port) |

### App Crashes

If your app is crashing, crash reports may help you determine the root
cause. Please see Apple's [Understanding and Analyzing Application Crash
Reports](https://developer.apple.com/library/content/technotes/tn2151/_index.html)
for more information about diagnosing iOS app crashes.

The SDK also supports automatic crash reporting for SDK-related crashes. When enabled via `webex.isCrashReportingEnabled = true`, the SDK detects if a previous crash involved an SDK-owned library and automatically uploads the relevant diagnostics on the next app launch. For details on requirements, crash attribution, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-ios-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.
