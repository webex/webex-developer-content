---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Request admin authorization'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/guest-to-guest-quickstart). [Full Markdown](../../../../docs/guest-to-guest-quickstart.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

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

## Step 3: Request admin authorization

After successfully registering the Service App, you are taken to a page that contains a Client ID and Client Secret. This is also where you request admin authorization for the Service App.

1.  Copy & paste the **Client Secret** value into a notepad for later use. Do note, this client secret is only shown once.
2.  Click the ‘Request admin authorization’ button and keep the browser tab open.
3.  In the next section, you will act as the administrator to authorize the app.
![admin request](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt87f7bf69cbe9c17c/690e467f358d8e67bb4c8f8f/img05_med.png?branch=integration)
