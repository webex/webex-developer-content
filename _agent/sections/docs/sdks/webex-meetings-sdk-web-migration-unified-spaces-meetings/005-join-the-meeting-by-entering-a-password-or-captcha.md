---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Join the Meeting by Entering a Password or Captcha
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-migration-unified-spaces-meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Limitations](011-limitations.md)

## Article introduction

This guide provides an overview of the improved meeting experience associated with spaces and outlines the impacted areas, along with the necessary adjustments in these areas for the adoption of these improved flows. 

## Selected section

## Join the Meeting by Entering a Password or Captcha

If the user is not part of the space where the meeting is created then the user will be prompted for the password. After multiple failed password attempts, captcha information is provided along with the appropriate error code. The user submits the captcha with the password to join the meeting successfully.
For more information, see:

- [Meeting Verify Password](https://webex.github.io/webex-js-sdk/api/#meetingverifypassword)
- [Password captcha flow](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-password-captcha)
