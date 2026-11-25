---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Error Code Handling
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-password-captcha.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed guide on implementing password and captcha verification flows. The flowchart below illustrates the complete process for implementing these flows, including the captcha refresh mechanism:

![Password Captcha Flow](https://user-images.githubusercontent.com/3918217/179780542-9f52c442-360e-4a0b-955f-603ab28489c3.png)

## Selected section

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
