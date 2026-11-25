---
type: Excerpt
canonical_url: https://developer.webex.com/docs/bots
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating a Webex Bot
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/bots). [Full Markdown](../../../../docs/bots.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Give Webex users access to outside services right from their Webex spaces. Bots help users automate tasks, bring external content into the discussion, and gain efficiencies.

[Create a Bot](<https://developer.webex.com/my-apps/new/bot>)

## Selected section

## Creating a Webex Bot

Creating a Webex Bot is super easy. If you're logged in, select [My Webex Apps](https://developer.webex.com/my-apps) from the menu under your avatar at the top of this page, click "Create a New App" then "Create a Bot" to start the wizard.

You'll be asked to provide some basic information about the bot: bot name, bot username, and an icon. These fields are end-user facing, so make them as descriptive as possible. Only the bot's first name will be shown when mentioned in messages, so try to avoid spaces in the bot name.  The description will be shown to users if you submit your bot to the [Webex App Hub](https://developer.webex.com/docs/app-hub-submission-process).



> **Warning**
>
> Webex App Hub is not supported for Webex for Government (FedRAMP)



Once you've filled out the registration form click "Add Bot", and if everything goes smoothly you're all set! You'll be given an access token for the new bot. This access token will be used to authenticate your bot with the Webex REST API.



> **Warning**
>
> The bot's access token will only be displayed once. Make sure to scroll down on the confirmation page, copy the token and keep it somewhere safe. If you misplace it, you can always generate a new one by finding the bot in [My Webex Apps](https://developer.webex.com/my-apps) and selecting "Regenerate Access Token" from the edit page.
