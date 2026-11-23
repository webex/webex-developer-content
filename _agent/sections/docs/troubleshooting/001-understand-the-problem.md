---
type: Excerpt
canonical_url: https://developer.webex.com/docs/troubleshooting
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Understand the Problem
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

## Understand the Problem

Check if the feature works in Webex without using the API. If you can reproduce the issue directly in Webex without API or SDK that should eliminate your application and in that case you should contact the [Cisco Technical Assistance Center (TAC)](https://www.cisco.com/c/en/us/support/web/tsd-cisco-worldwide-contacts.html) to report the issue.

If the problem is with the API or SDK, focus on narrowing the scope of the issue. Is it an internet connectivity issue, incorrect API response or behavior, are you receiving a non-successful HTTP response status code (such as 4xx or 5xx), or an authentication error?

### Verify Network Connectivity

Ensure your device or server has internet access and can reach the Webex servers. For webhook endpoints receiving HTTP requests from Webex, verify that your devices or web server is accessible from the internet. For more details about the network and internet requirements for the Webex service please refer to the [Webex Network Requirements](https://help.webex.com/en-us/article/WBX000028782/Network-Requirements-for-Webex-Services) guide for more details.

### Review Authentication

Confirm that your authentication credentials (such as API keys, Client ID, Client Secret, or tokens) are correct and have not expired. If you are using an Access Token from an Integration or Service App you can make a GET request to `https://webexapis.com/v1/people/me` to verify the Access Token is working (you will need to have the `spark:people_read` scope for this API). Verify that any Webex user account being used can login to Webex.

### Check the Documentation

Always refer to the API documentation to ensure you're using the correct endpoints, methods, and parameters. This would also be a good time to check with the [AI Assistant for Developers](https://developer.webex.com/admin/docs/webex-aI-assistant-for-developers?ai-assistant-is-docked-window=true) for code generation guidance or to locate relevant documentation and APIs.

### Review Recent Changes

Check for any recent changes in your code or the API that might have caused the issue. Look at the API change log ([Webex Suite](https://developer.webex.com/admin/docs/api/changelog/webex-admin), [Webex Contact Center](https://developer.webex.com/webex-contact-center/docs/api/changelog/webex-contact-center)) well as the documentation for the individual requests/endpoints being used by your application for updates. Verify that your software or SDK version is up to date and still supported by reviewing the [Webex API and SDK Support Policy](https://developer.webex.com/docs/webex-api-and-sdk-support-policy).

### Consult Logs and Error Messages

Examine your server logs or application error logs for additional insights. When the Webex REST API returns an HTTP Error code response the HTTP Response body will provide more details about the cause of the error including a `trackingID` we can use to locate your issue in our logs, so it is important to log the HTTP Response body when an error is encountered.

### Test with Simplified Requests

Simplify your requests to the bare minimum required fields as indicated in the API Documentation to help isolate the problem.

### For SDK Related Issues Attempt to Reproduce Problems in our Sample Apps

Reproducing your issues using our sample apps can help determine whether the problem lies with our SDK or is an implementation issue in your code. You may be able to resolve your implementation issues by referring to the source code of these samples:

- [Embedded App SDK Kitchen Sink](https://eaf-sdk.webex.com/index.html#kitchen-sink-app)
- [Browser JS SDK Samples](https://web-sdk.webex.com/)
- [iOS SDK Sample](https://github.com/webex/webex-ios-sdk-example)
- [Android SDK Sample](https://github.com/webex/webex-android-sdk-example)
- [Webex Contact Center Widget/Desktop SDK Samples](https://github.com/WebexSamples/webex-contact-center-api-samples/tree/main/widget-samples)
