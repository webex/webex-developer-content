---
type: Excerpt
canonical_url: https://developer.webex.com/docs/troubleshooting
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Collect Browser, SDK and Device Logs
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/troubleshooting). [Full Markdown](../../../../docs/troubleshooting.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Facing issues with Webex APIs or SDKs? Follow this proven troubleshooting process, and we promise you'll quickly identify the root cause and get back on track in a jiffy.

---

This guide provides a structured, methodical approach to diagnosing and resolving issues within your Webex API and SDK implementations. It is designed to equip developers with the essential steps for self-service troubleshooting, enabling you to systematically identify root causes, validate hypotheses, and leverage available resources. When self-resolution isn't possible, this document further outlines best practices for effectively engaging Webex Developer Support, ensuring that you can articulate your issue with precision and receive timely, targeted assistance.

An example workflow would look like:

1. **Initial Check**: First see if the feature works directly within Webex, without relying on the API or SDK. This helps isolate the problem.
1. **Questioning the Changes**: Ask yourself if you or your fellow app maintainers have made any recent changes to the app, network, or infrastructure that could be affecting functionality.
1. **Investigate and Review**: Dive into documentation and examine network access, internet connectivity, and user login and OAuth details to pinpoint potential reasons for the issue.
1. **Testing Hypotheses**: Analyze your application logs and perform simple API requests to test your theories and identify the main cause.
1. **Consulting Help**: Leverage the [AI Assistant for Developers](https://developer.webex.com/admin/docs/webex-aI-assistant-for-developers?ai-assistant-is-docked-window=true) for code generation guidance or to locate relevant documentation and APIs.
1. **Understanding Results**: Review the gathered information to understand the outcomes. This will be useful if you need to reach out to Webex for further support.

## Selected section

## Collect Browser, SDK and Device Logs

For Browser based issues including browser SDKs please follow the steps below to enable and collect logs.

### Open Developer Tools

Each Browser will have different ways to open the Developer Tools which may change between their releases, so it is best to reference the browsers documentation as much as possible:

- **Google Chrome**: [https://developer.chrome.com/docs/devtools/open](https://developer.chrome.com/docs/devtools/open)
- **Microsoft Edge**: [https://learn.microsoft.com/en-us/microsoft-edge/devtools/overview#open-devtools](https://learn.microsoft.com/en-us/microsoft-edge/devtools/overview#open-devtools)
- **Firefox**: [https://firefox-source-docs.mozilla.org/devtools-user/#the-core-tools](https://firefox-source-docs.mozilla.org/devtools-user/#the-core-tools)
- **Safari**: [https://developer.apple.com/documentation/safari-developer-tools/develop-menu](https://developer.apple.com/documentation/safari-developer-tools/develop-menu)

### Enable Optional Logging Features in Developer Tools

Before duplicating your browser-based issues the following settings may be needed to ensure the logs contain all the necessary information to troubleshoot your issues.

Please enable the following in the Console settings:

1. **Timestamps**
1. **Preserve Log**
1. **Log XMLHTTPRequests** (Chrome and MS Edge only)

You should also enable **Preserve Log** in the Network settings.

Once these settings are enabled you can begin collecting logs while you reproduce the issues you are experiencing with our API or SDK.

### Capture the HAR Logs

For most popular browsers you can follow the [Generate a HAR File in Your Browser](https://help.webex.com/en-us/article/WBX9000028670/Generate-a-HAR-File-in-Your-Browser#id_90869) guide in our Webex Help website to capture and save the HAR(HTTP Archive) log while duplicating your problem. If you do not see your browser listed here please reference the documentation provided by the browser developer for guidance on collecting logs.

### Capture the Console Logs

With the Developer Tools panel open (see instructions above) click on the **Console** tab. After reproducing the issue right-click within the console output and select **Save as** or **Save all**... to export the log to a file.

### Enable Additional logging in the Webex Browser JS SDKs

If your issues are related to the Webex JavaScript based SDK’s it is also important to increase the log level to `info` or `debug` for you to capture additional logging details. The added logging will increase the size of the logs generated by your application, so it’s not usually recommended to set the log levels once you have deployed your application to your production environment.

For the Webex Meetings and Messaging features of the SDK see the “Change the Log Level Within Your App” content in the [Troubleshooting](https://developer.webex.com/docs/sdks/browser#troubleshooting) section of our Browser SDK Guide. To set the log level for our Webex Calling SDK see the Logger Configuration content in the Webex Calling [Configuration Details](https://developer.webex.com/calling/docs/sdks/webex-calling-sdk-web-quickstart#calling-configuration-details) section of our Web SDK Quickstart guide.

### Capture WebRTC Dump Logs for WebRTC (Web Real-Time Communication) Media Issues in the JavaScript SDK

Collecting WebRTC dumps and other related logs can be valuable for diagnosing issues with WebRTC in your application. Below we have provided the instructions for doing so in Google Chrome, Microsoft Edge, Firefox, Safari. By following these instructions, you can collect WebRTC dump logs for further analysis and troubleshooting in each of these major browsers. Please also note that the location and availability of these settings may change with updates to the browsers, so you may need to reference the documentation provided by the Browser developer.

#### Google Chrome and Microsoft Edge

1. In a new tab, Open WebRTC Internals. For Chrome enter `chrome://webrtc-internals/` in the address bar and press Enter. For Microsoft Edge enter `edge://webrtc-internals/` in the address bar and press Enter.
1. Start your Webex Call or Meeting using the Webex JavaScript SDK in another tab to initiate the WebRTC Session.
1. After duplicating issue and while call is still active, return to the WebRTC Internals tab click the **Create a WebRTC-Internals dump**.
1. Click the **Download the "webrtc-internals dump"** button to save a file containing the WebRTC logs and statistics.

#### Mozilla Firefox

1. In a new tab, type `about:webrtc` in the address bar and press Enter.
1. Enable Auto Refresh in all fields if not already enabled.
1. Start your Webex Call or Meeting using the Webex JavaScript SDK in another tab to initiate the WebRTC Session.
1. After duplicating issue and while call is still active, return to the tab with `about:webrtc` already opened.
1. Click the **Save Page** button at the bottom of the page and save the file.

#### Apple Safari

1. Open the JavaScript Console from the Develop menu.
1. Go to the Web Inspector Settings (gear icon) in upper right corner.
1. On the Console Settings tab and ensure WebRTC logging is set to Verbose.
1. Click on the Console tab in the Web Inspector.
1. Start your Webex Call or Meeting using the Webex JavaScript SDK in another tab to initiate the WebRTC Session.
1. After duplicating issue click in the Console and use keyboard combination Cmd + A to select all followed by Cmd + S to save to a file.

### Collect Embedded Apps Logs

Please attempt to duplicate your issues in our sample apps as well (see the list of Samples here: Sample Apps) to verify if your issues are specific to our SDK. If you cannot resolve your issues by referencing our Sample Apps or have experienced the same issues in our Sample App, please follow the instructions below for collecting logs before reporting the issue to Developer Support.

For instructions on enabling and opening Developer Tools for the Webex Apps and different Operating systems please follow the instructions [Embedded App Developer guide](https://developer.webex.com/create/docs/embedded-apps-guide#enabling-developer-tools) On the Webex Developer Portal. Once enabled you can follow the Capture HAR logs and Capture Console logs just like you would in a regular web browser, like mentioned in our Browser SDK content above to gather the logs while duplicating your issue with our Embedded Apps feature including the related SDK.

Like the other JavaScript based SDK’s the log levels can also be changed as described in the [Embedded Apps reference guide](https://eaf-sdk.webex.com/#log-levels).

### Collect Mobile SDK Logs

Before collecting logs, it is always recommended to attempt to replicate problems using our sample applications (see the list of Samples here: Sample Apps) to determine if the issues are specific to the SDK or your implementation.

If you cannot resolve your issues by referencing our Sample Apps or have experienced the same issues in our Samples, please follow the instructions below for collecting logs on both Android and iOS SDKs before reporting the issue to Developer Support.

#### iOS SDK

To effectively troubleshoot the Webex iOS SDK, several methods are available to enable additional logging and gather logs.

First, you can refer to the detailed instructions provided on the [iOS SDK Overview](https://developer.webex.com/meeting/docs/sdks/ios-sdk-overview#troubleshooting-the-ios-sdk) Webex Developer page to enable additional logging. To obtain logs directly from the device using Xcode, see our [guide on GitHub](https://github.com/webex/webex-ios-sdk/wiki/Extracting-SDK-and-WME-logs) which outlines the process.

The SDK also includes the `webex.getLogFileUrl()` ([reference guide](https://webex.github.io/webex-ios-sdk/Classes/Webex.html#/s:8WebexSDK0A0C13getLogFileUrl10Foundation3URLVSgyF)) function for programmatically gathering logs. For sample code demonstrating how to implement the `webex.getLogFileUrl()`  function and attach the log file to an email, you see it’s usage in the [Webex iOS SDK sample application](https://github.com/webex/webex-ios-sdk-example/blob/master/KitchenSink/Controllers/HomeViewController.swift#L462) on GitHub.

In the event of app crashes, analyzing crash reports can be crucial for identifying the root cause. Apple's guide [Diagnosing issues using crash reports and device logs](https://developer.apple.com/documentation/xcode/diagnosing-issues-using-crash-reports-and-device-logs) offers valuable insights into diagnosing iOS app crashes effectively.

The SDK also supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. Additionally, the SDK can automatically detect SDK-related crashes and upload the relevant diagnostics on the next app launch when enabled via `webex.isCrashReportingEnabled = true`. For full details on these APIs, including response handling, requirements, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-ios-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

#### Android SDK

Like our other Mobile SDK’s, the Webex Android SDK provides settings to control the logging level of the logs generated by our SDK for troubleshooting purposes. To capture comprehensive logs during troubleshooting set the log level to verbose using the `webex.setLogLevel(Webex.LogLevel.VERBOSE)` function.

You can also use `webex.getlogFileUri()`([reference guide](https://webex.github.io/webex-android-sdk/dokka-docs/com.ciscowebex.androidsdk/-webex/getlog-file-uri.html)) function from the SDK to get a file URI where all the logs are stored. We also provide an example demonstrating how to gather logs into an email for Android located here in our [Android SDK Sample Application](https://github.com/webex/webex-android-sdk-example/blob/master/app/src/main/java/com/ciscowebex/androidsdk/kitchensink/HomeActivity.kt#L166-L187) on GitHub.

The SDK also supports uploading diagnostic logs directly to the Webex backend using `webex.uploadDiagnosticLogs()`, eliminating the need to manually extract and share log files. Additionally, the SDK can automatically detect SDK-related native crashes and upload the relevant diagnostics on the next app launch when enabled via `webex.enableCrashReporting(true)` (requires Android 12+ / API 31+, release builds only). For full details on these APIs, including response handling, requirements, and limitations, see the [SDK Diagnostics Log Upload](https://github.com/webex/webex-android-sdk/wiki/SDK-Diagnostics-Log-Upload) wiki guide.

Additionally, the Android system logger utility (Logcat) can be used to collect logging from the Android system which can be useful for troubleshooting. You can use the Logcat command-line tool to collect, view, and filter all logs. See the Write and View Logs with Logcat contents for more information ([https://developer.android.com/studio/debug/am-logcat](https://developer.android.com/studio/debug/am-logcat)).

Further Android Developer documentation for logcat usage is available at:

- [https://developer.android.com/tools/logcat](https://developer.android.com/tools/logcat)
- [https://developer.android.com/studio/debug/logcat](https://developer.android.com/studio/debug/logcat)

### Collect Device/RoomOS Logs

To gather logs from Webex Device or RoomOS, please refer to the detailed instructions provided in the [Collecting Logs from Webex Cloud Video Devices](https://www.cisco.com/c/en/us/support/docs/collaboration-endpoints/webex-desk-limited-edition/220725-collect-logs-from-webex-cloud-video-devi.html) guide on the Cisco Support site.

For issues related to Macros, it is crucial to review and share the console history available in the Macro Editor on the device's local web portal. This can provide insights into any errors or unexpected behavior. For further information and guidance, consult the [Macro tutorial](https://roomos.cisco.com/doc/TechDocs/MacroTutorial).
