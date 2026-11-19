---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 1: Obtain and set up a Developer G2G Sandbox'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-to-guest-quickstart). [Full Markdown](../../../../docs/guest-to-guest-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Step 3: Request admin authorization](003-step-3-request-admin-authorization.md)

## Article introduction

This tutorial provides step-by-step instructions to set up a Webex Service App that enables organizations to create and manage guest-to-guest meetings with unique join links for non-licensed users.

---

Webex Guest-to-Guest (G2G) Meetings apps are created to facilitate full-featured Webex meetings for non-licensed users, with a Webex Service App acting as the orchestrator. This approach offers flexibility by not requiring individual user licenses, instead allowing organizations to pay for simultaneous meeting sessions, making it ideal for scenarios where participants only need occasional access to Webex meetings. G2G meetings opens a variety of new application use cases, such as virtual consultations (e.g., doctor-patient, customer support), real-time expert assistance, and home care support, where participants are typically not permanently licensed Webex users.

This quickstart guide is a tutorial for developers who are just starting to get acclimated with creating and deploying G2G meetings apps. For full documentation on Guest-to-Guest Meetings Apps, please refer to the [Guest to Guest Developer Guide](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide).

Upon completion, you will be able to:

- Obtain a Developer Sandbox for Guest-to-Guest Meetings.
- Create a Webex Service App to facilitate a G2G Meetings demo.
- Request an admin to authorize the Service App.
- Act as the admin that authorizes the Service App in Control Hub.
- Retrieve an access token for the sample G2G Meetings app.
- Configure the G2G Meetings app with an access token and explore the sample Python code.
- Run the sample app to create and start a meeting between guest users.

We will be using a Python-based demo app that correlates to a variety of use cases where temporary, on-demand meeting access is needed for external participants. The app allows you to configure and start guest-only meetings, demonstrating how to generate unique host and guest join links. It also showcases the creation of guest identities, enabling non-licensed participants to easily access and join meetings.

## Selected section

## Step 1: Obtain and set up a Developer G2G Sandbox

You will first need to have administrator access to a Webex organization that is licensed for Guest-to-Meetings to complete this tutorial. The good news is that we offer developers a sandbox that provides all of this for free. Simply click the green “Request a Guest-to-Guest Sandbox” button on [this page](https://developer.webex.com/docs/g2g-sandbox) to have one assigned to a personal email address. When the sandbox has been provisioned, you will be sent administrator credentials that you can use to create and deploy the demo G2G app.

For this tutorial, and other use cases where a meeting “host” needs other participants to bypass the lobby and join the meeting directly, there some settings that should be configured in the G2G sandbox:

1.  Open a new browser tab and navigate to Webex Control Hub: [admin.webex.com/login](https://admin.webex.com/login)
2.  Log in to Control Hub with the sandbox admin credentials that you were assigned.
3.  Under **Services**, select “Meeting”.
4.  On the Meeting Sites page, select your sandbox org name.
5.  On the sandbox site page, select the “All” tab, then select “Security” from the drop-down menu.
6.  In the “Webex meeting security” section, make sure “Join meeting directly” is selected for both “how external invitees join meetings” and “how to manage people who aren't invited or aren't signed in when they attempt to join meetings”. These settings allow guests to use the `attendeeLink` to join and start the meeting even if they aren’t the host.
![meeting security](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1d5922014e43b351/690e467f614c499ffe613588/img01_med.png?branch=integration)
7.  Scroll down to the “Attendees” section and enable the option to “Allow attendees or panelists to join before host (Meetings, Training and Events)”. This allows any guest attendee to join the meeting without the host.
![meeting security attendees](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3312e041ffc98b17/690e467fa62c1d5372655f90/img02_med.png?branch=integration)
8.  Save the settings before exiting.
