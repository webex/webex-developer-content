---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Password and Captcha Verification Process
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-password-captcha.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed guide on implementing password and captcha verification flows. The flowchart below illustrates the complete process for implementing these flows, including the captcha refresh mechanism:

![Password Captcha Flow](https://user-images.githubusercontent.com/3918217/179780542-9f52c442-360e-4a0b-955f-603ab28489c3.png)

## Selected section

## Password and Captcha Verification Process

When the SDK is configured with `meetings.experimental.enableUnifiedMeetings` set to `true`, the SDK leverages the Webex API to fetch meeting details. 

```js
Password required. Call fetchMeetingInfo() with password argument
```

or

```js
Captcha required. Call fetchMeetingInfo() with the captchaInfo argument
```

In cases where access is restricted, the Webex API returns specific error codes, such as 403xxx and 423xxx. In response to those errors, you must:

1. Provide the correct password or captcha.
1. Call `fetchMeetingInfo` again to retrieve the meeting information.



> **Info**
>
> For scheduled space meetings where you're neither a space member nor an invited participant, a password prompt is provided. After multiple incorrect password attempts, captcha verification is triggered.



For more information see the [Kitchen Sink app](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings/).
