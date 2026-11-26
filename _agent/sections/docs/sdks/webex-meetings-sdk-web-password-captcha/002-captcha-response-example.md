---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Captcha Response Example
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-password-captcha.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article provides a detailed guide on implementing password and captcha verification flows. The flowchart below illustrates the complete process for implementing these flows, including the captcha refresh mechanism:

![Password Captcha Flow](https://user-images.githubusercontent.com/3918217/179780542-9f52c442-360e-4a0b-955f-603ab28489c3.png)

## Selected section

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
