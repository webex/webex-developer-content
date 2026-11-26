---
type: Excerpt
canonical_url: https://developer.webex.com/docs/troubleshooting
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'If You’re Still Stuck: Engage Developer Support'
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

## If You’re Still Stuck: Engage Developer Support

If you have not resolved your issue at this stage, it is likely time to open a ticket with Developer Support. With the guidance provided below, document the issue, environment details, and steps to reproduce the issue and API response trackingID. Once you have gathered all the necessary information open a [Developer Support](https://developer.webex.com/support) ticket using the Support option provided in the navigation menu at the top of this page.

### Best Practices for Reporting Issues

Before engaging Webex Developer Support, it is important to gather and provide as much details as possible of the issues you are experiencing. This will improve the quality of support you are provided and reduce the time needed to help identify and resolve your issue.

If you are having multiple issues, it is very important to separate those issues into individual tickets to avoid any misunderstanding or confusion. Some issues may take longer to resolve which is another reason to open one ticket per issue.

When reporting issues to Webex Developer Support please format your content as shown below.

### Description

Provide a concise description of the issue being experienced.

### Environment

Issues can appear in a particular environment and not others. For example, you may encounter issues when running the website on Firefox, or an app malfunctions only when running on an iPhone X. These issues can only be identified with cross browser, OS, or device tests.

Within this environment section please provide the following details:

1. **Device Type/Model**: Hardware and specific device model.
1. **OS**: Operating System name and version.
1. **Software type, name, and/or version**: Provide details about the software (application/browser, sdk, or coding language) which is being tested, and in which the issue has appeared.
1. **User or Tester**: Name and email of the user who encountered the issue.
1. **Connection Type/Strength**: If the issue is dependent on the internet connection (4G, 3G, Wi-Fi, Ethernet, VPN, Proxy) mention the connection type and strength at the time of testing.
1. **Rate of Reproduction**: Specify the frequency (intermittent or continuous) and the number of times the issue has been reproduced.
1. **Prerequisites**: List any specific conditions or setups required before reproducing the issue, such as user permissions, necessary configurations, or data states.

### Steps to Reproduce

Provide a numbered list of detailed steps taken that produced the issue you are reporting so that Developer Support can follow them precisely and see the issue for themselves. It is also important to provide both the expected results from following the steps and a clear description of the actual results where the issue is observed. The Actual Results should include as much details as possible, including error messages, screenshots, or screen recordings when possible.

### Logs and Visual Proof of Issue

To effectively troubleshoot issues, it's important to gather logs from the SDK, application, or API requests and responses, depending on the type of problem you're encountering. API responses typically include a tracking ID, which assists in locating relevant logs in Webex to address your concerns.

When an error response is generated, the API usually embeds the tracking ID within the JSON body of the HTTP response. However, in some instances, particularly when a successful `HTTP 200` status code is returned, the tracking ID may not appear in the response body. In such cases, you'll need to examine the HTTP response headers for a `trackingId` header, which should contain the tracking ID value.

Rest API response example showing `trackingId` location in Header and response body:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9d4ca9721d314871/troubleshooting-the-suite-apis-1.png)

For issues affecting user experience (UX), it is advisable to provide screen recordings or screenshots of the problem, accessible via [Vidcast](https://vidcast.io/) or your preferred screen recording utility.

### Template for reporting issues to Developer Support

Please use this template along with the guidance above when reporting issues. This template provides a comprehensive structure for reporting issues, ensuring clarity and completeness in communication with our teams.

Following these steps will help facilitate effective troubleshooting by the Webex Developer Support team. Adjust elements as necessary based on the actual issue and environment details.

**Notes**:

- Be sure to fill in placeholders with specific information relevant to your issue.
- Include as much detail as possible in descriptions and logs for better troubleshooting.
- Review the template for completeness and accuracy before submitting your ticket.
- For details on collecting logs, see the following section, “Collect Browser and SDK Logs” below.

### API Support Template

Use this template for your API support requests:

```text
Description: [concise description of issue]
Environment: 
  Device Type/Model: [Device manufacturer, model, and version]
  OS: [computer, mobile, or device Operating System]
  Software type, name, and/or version: [Provide details about the software used when issue was encountered]
Tester/Affected User: [Name/email of the user who encountered the issue]
Connection Type/Strength: [Internet/network Connection type and other detail like VPN/Proxy involvement]
Rate of Reproduction: 
  [frequency (intermittent or continuous) and Rate issue is occurring]
Prerequisites: 
  [Prerequisites/Conditions resulting in issue]
Steps to Reproduce:
    1.[step 1 description]
    2.[step 2 description]
    3.[step 3 description]
    4.[repeat additional steps as needed with as much detail as possible]
  Expected Results:
    [provide description of the expected results/behavior]
  Observed Results:
    [provide description of the actual results being experienced]
Attach Logs and other supporting materials:
    [screen recording, screenshots, sample code, etc]
```

### Example Request Template

Here is an example of a completed template reporting an issue to Webex Developer Support. This example demonstrates how to fill out the template with specific details of an issue being reported to Developer Support.

```text
Description:
  The Open Together functionality fails to direct users to the dashboard page, presenting a "404 Not Found" error instead.

Environment:
  Device Type/Model: Apple iPhone X
  OS: iOS 14.4
Software/Development Language Details: Webex embedded app SDK version 1.3.5 in Webex App 45.3.1
Tester/Affected User: John Doe, johndoe@example.com
Internet/Network Connection Type and Other Details: Wi-Fi with VPN enabled

Rate of Reproduction:
  Continuous; reproduced every time login is attempted

Prerequisites/Conditions Resulting in Issue: 
  User must be connected to VPN; only occurs when VPN is active

Steps to Reproduce:
  1.Open Browser:
    Launch Webex Meeting on the iPhone X.
  2.Navigate to Embedded app:
    Open “Example” Embedded App from Apps panel in meeting.
  3.Launch Feature page:
    Click on component located in main menu of embedded app home page.
  4.Perform Action:
    Click on the "Open Together" button located at bottom of embedded app.
  5.Check for result in participant view:
    Observe the Embedded Apps behavior after submitting the shared page loads.

Expected Results:
  After clicking "Open Together", the participants Meeting App should open the embedded app to the shared URL [https://www.example.com/dashboard].
  The dashboard should display a welcome message, "Welcome, John Doe!".

Observed Results:
  After clicking "Submit", the user is redirected to an error page with the URL [https://www.example.com/error].
  The error page displays a message, "404 Not Found".

Attached Logs and Other Supporting Materials:
  Screen Recording: A recording of the login process showing the issue can be accessed here: https://vidcast.io/example-login-error.
  Screenshots: Included are screenshots of the error page.
  Sample Code and logs: Attached logs and snippet of the JavaScript code used for the Open Together functionality.
```
