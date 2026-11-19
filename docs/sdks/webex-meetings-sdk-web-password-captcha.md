---
type: Guide
title: Web Meetings SDK | Implementing Password and Captcha Verification Flows
display_title: Passwords & Captchas
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha)

This article provides a detailed guide on implementing password and captcha verification flows. The flowchart below illustrates the complete process for implementing these flows, including the captcha refresh mechanism:

![Password Captcha Flow](https://user-images.githubusercontent.com/3918217/179780542-9f52c442-360e-4a0b-955f-603ab28489c3.png)

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

## Captcha Response Example

A typical captcha response includes fetching the captcha image and audio, as well as refreshing the captcha URL:

```javascript
{
  "code": 423006,
  "message": "PasswordOrHostKeyError too many times, please input captcha code",
  "captchaID": "Captcha_8f7ecfce-541f-4f22-9ff7-a42d6a323336",
  "verificationImageURL": "https://train.qa.webex.com/captchaservice/v1/captchas/Captcha_8f7ecfce-541f-4f22-9ff7-a42d6a323336/verificationCodeImage",
  "verificationAudioURL": "https://train.qa.webex.com/captchaservice/v1/captchas/Captcha_8f7ecfce-541f-4f22-9ff7-a42d6a323336/verificationCodeAudio",
  "refreshURL": "https://train.qa.webex.com/captchaservice/v1/captchas/refresh?siteurl=train&captchaID=Captcha_8f7ecfce-541f-4f22-9ff7-a42d6a323336"
}
```

## Error Code Handling

While the Webex API returns various error identifiers, it primarily checks for 403xxx and 423xxx codes. Those codes indicate password and captcha errors, specifically:

```js
const PASSWORD_ERROR_DEFAULT_MESSAGE =
  'Password required. Call fetchMeetingInfo() with a password argument';
const CAPTCHA_ERROR_DEFAULT_MESSAGE =
  'Captcha required. Call fetchMeetingInfo() with a captchaInfo argument';
const ADHOC_MEETING_DEFAULT_ERROR =
  'Failed to start the ad-hoc meeting, Please contact support team ';
```

For more information, refer to [Webex JS SDK](https://github.com/webex/webex-js-sdk/blob/master/packages/%40webex/plugin-meetings/src/meeting-info/meeting-info-v2.js).

### Password Error Details

The following table lists password error codes and descriptions of when these codes are returned.

| **Error Code** | **Description** |
| --- | --- |
| `403036` | Access to the meeting is blocked without a password or host key. |
| `403004` | Joining the meeting requires a password or PIN. |
| `403028` | Access denied due to an incorrect password. |

### Captcha Error Details

The following table lists captcha error codes and descriptions of when these codes are returned.

| **Error Code** | **Description** |
| --- | --- |
| `423006` | Multiple incorrect password attempts have triggered a captcha verification. |
| `423001` | Excessive invalid access attempts trigger a captcha requirement. |
| `423005` | Repeated password errors result in a prompt for captcha input. |
