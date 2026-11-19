---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-sdk-overview
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Troubleshooting the Android SDK
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-sdk-overview). [Full Markdown](../../../../../docs/sdks/android-sdk-overview.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Requirements](006-requirements.md)

## Article introduction

Build Android apps with the **Webex Android SDK**. Find supported features, requirements, samples, and API references.

## Selected section

## Troubleshooting the Android SDK

If you're having trouble with the Android SDK, here's some more information to help troubleshoot the issue.

### View the System Logs

The Webex Android SDK uses the Android system logger utility to collect log messages that will allow you to define problem areas when troubleshooting.

Use the `Logcat` command-line tool to collect, view, and filter all SDK logs. The Android SDK provides the option to display all messages or just the messages that indicate the most severe errors. Set the log level to `verbose` to display all errors. See [Write and View Logs with Logcat](https://developer.android.com/studio/debug/am-logcat.html) for more information.

```java
webex.setLogLevel(Webex.LogLevel.VERBOSE)
```
### Upload Diagnostic Logs

The SDK supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. The uploaded bundle contains the same SDK diagnostic logs, media engine logs, and any pending crash reports that are available through the existing `webex.getlogFileUri()` API. For full details including response handling and error codes, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-android-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

### Firewall Ports

The Android SDK makes use of the following network ports. If you're encountering connection issues, make sure there aren't any firewalls blocking or preventing communication over these ports:



| Service | Protocol | Port(s) |
| ------- | -------- | ------- |
| Messaging | HTTPS | 443 |
| Notifications | WebSocket | 443 |
| Calls | HTTPS | 443 |
| Media | RTP/SRTP over UDP/TCP | 33434-33598, 8000-8100 or 33434 (shared port) |

### SDK Dependencies

For more information about dependencies of the Android SDK, please refer to their documentation:

* [Troubleshoot Android Studio](https://developer.android.com/studio/troubleshoot.html)
* [Android SDK Tools](https://developer.android.com/studio/command-line/index.html)
* [JDK Troubleshooting Guide](https://docs.oracle.com/javase/7/docs/webnotes/tsg/)
* [Gradle User Guide](https://docs.gradle.org/current/userguide/userguide.html)

### App Crashes

If your app is crashing, running a stack trace may help you determine the root cause. Please see Android’s [Diagnose the Crashes](https://developer.android.com/topic/performance/vitals/crash.html#diagnose_the_crashes) for more information about determining the cause of Android app crashes.

The SDK also supports automatic crash reporting for SDK-related native crashes. When enabled via `webex.enableCrashReporting(true)`, the SDK detects if a previous crash involved an SDK-owned library and automatically uploads the relevant diagnostics on the next app launch. This feature requires Android 12+ (API 31+) and is only available on release (non-debuggable) builds. For details on requirements, crash attribution, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-android-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.
