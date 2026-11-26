---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Create a Service App'
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

## Step 2: Create a Service App

Webex G2G Meetings can only be facilitated through a Service App. Now that you have a sandbox set up, we can create the Service App. Here are the basic steps for creating one:

1.  In a new browser tab, log in to `developer.webex.com` with the admin credentials that were provided for your G2G Sandbox. Alternatively, you can create another user in your sandbox to be the developer.
2.  Up on the top right corner of the page, click your avatar and then select ‘My Webex Apps’.
3.  On the ‘Create a New App’ page, find the **Service App** card and click the ‘Create a Service App’ button.
![Service Apps](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt735443031a3e9f18/690e2768b5ec5732b6b86e64/img03_small.png?branch=integration)
4.  Fill out the webform to register a new service app.
    *   **App name**: use something like “G2G Meetings Tutorial”.
    *   **Icon**: can be any selection.
    *   **Description**: “Testing a G2G Meetings App”
    *   **Contact Email**: Use the email from the account you logged in with.
    *   **Scopes**: Select the following scopes for the guest-to-guest sample app (use the browser’s “find” to quickly jump to each scope):
        *   `meeting:schedules_read`
        *   `meeting:schedules_write`
        *   `guest-meeting:rw`
![scopes](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltba0f272379a6fe56/690e2809da37a80f80d0b275/img04_small.png?branch=integration)
5.  Click the ‘Add Service App’ button to finish registration.
