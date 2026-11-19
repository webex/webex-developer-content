---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 8: Launch and use the G2G meetings demo app'
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

## Step 8: Launch and use the G2G meetings demo app

Now that the app is deployed and configured, let’s get it started.

1.  Go back to command line window in the `webex-g2g-app` directory.
2.  Launch the app using the following command:
    ```bash
    flask run
    ```
3.  If successful, you will see a response with a localhost URL like this:
    ```bash
    Running on http://127.0.0.1:5000
    ```
4.  Next, open a browser tab and navigate to that localhost URL.
5.  You now should see the Guest-to-Guest Meeting Helper screen in the browser, which is where the meeting will be configured.
6.  Complete the steps as shown in the illustration below:
    - (1) Type in any meeting title. 
    - (2) Use the default date & time that is auto filled. Also, if you select “Yes” for “Join Before Host”, it allows the “join link” to be used immediately without having to start the meeting first.
    - (3) The Meeting Outcome section is read-only information.
    - (4) Make two guest users.
    - (6) Before starting the meeting, right-click and copy the “Join Meeting” link for the 2nd meeting guest to use after the meeting starts.
    - (5) Click the Start Meeting link to launch the meeting in your browser.
![demo app](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5a4b890adbee27de/690e43c19ff6838a46a742fa/img10_med.png?branch=integration)
7.  To test a guest-only meeting scenario by yourself, open an incognito browser tab and paste the join link (6) URL in the address bar.

Finishing that last step with a guest-only meeting means you successfully completed this Quickstart Guide and gained hands-on experience with building a Webex G2G application. You've learned how to configure a G2G sandbox in Webex Control Hub, create and authorize a Service App with the required scopes for guest meetings, and retrieve the access token. Additionally, you've successfully deployed and configured a Python demo app that leveraged the Webex APIs to set up a meeting, create distinct guest identities, and generate the unique join links essential for non-licensed participants.
