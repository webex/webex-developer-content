---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sandbox_cc
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Sandbox Contents
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sandbox_cc). [Full Markdown](../../../../docs/sandbox_cc.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

To request or manage a Contact Center sandbox, open the [official portal page](<https://developer.webex.com/docs/sandbox_cc>) and sign in.

## Selected section

## Sandbox Contents

Every sandbox requested from the developer portal has the following features configured so that you can test all Contact Center features end to end:

1. **Webex calling for Voice** - Webex calling is the default calling platform. You use the main PSTN number as the entry point for contacting an agent logged into the Agent Desktop. The main PSTN number can be found in your sandbox provisioning email.
1. **Administrator** - One (1) administrator user is configured. Details are available in your sandbox provisioning email.
1. **Desktop Profiles** – Two desktop profiles are created, one with and one without auto-wrap-up enabled (the auto-wrap-up profile ends the call with a default wrap-up code rather than requiring an agent choice).
1. **Agents/Users** – Two default user are configured:

    - Premium Agent 1 who only has access to Agent Desktop functions.
    - Supervisor Agent 2 who has access to additional supervisory metrics and functions.

    Details are available in your sandbox provisioning email.

1. **Team** - A default agent-based team is available for use.
1. **Multimedia profile** - One (1) default multimedia profile is available.
1. **User profiles** - Five (5) pre-configured [user profiles](https://help.webex.com/en-us/article/n5jdj19/Webex-Contact-Center-administrator-roles-and-privileges) are available:

    - Administrator Only Profile
    - Administrator Profile
    - Premium Agent User Profile
    - Standard Agent User Profile
    - Supervisor Profile

1. **Queue** - One (1) inbound voice queue is preconfigured.
1. **Audio files** - Default hold music as well as a greeting message are preconfigured.
1. **Flow** - A default basic flow is configured to play a default hold music and redirect the call to the default inbound queue.
1. **Business Hours** – Business hours (defined collections of operational hours enabling you to route calls to agents who are actually in the office) have been mapped to the default inbound entry point and the default basic flow that is active for 60 days from the time of creation.
