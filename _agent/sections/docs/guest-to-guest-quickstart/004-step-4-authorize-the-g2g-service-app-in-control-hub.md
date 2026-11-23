---
type: Excerpt
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: Authorize the G2G Service App in Control Hub'
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

## Step 4: Authorize the G2G Service App in Control Hub

Act as the Webex admin to authorize your own Service App in Control Hub.

1.  Go back to the Webex Control Hub site or open a new browser tab and navigate to: `admin.webex.com/login`
2.  Log in with the sandbox admin credentials that you were assigned.
3.  Inside Control Hub, under the **Management** section in the left menu, select **Apps**.
4.  Once on the Apps page, select the **Service Apps** tab.
5.  Find the Service App name you just created and click on it. This will open the description of the Service App.
![Apps in CH](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt157903690e0c32bf/690e467f6b2a06fa7b470155/img06_med.png?branch=integration)
6.  In the Service App description window, click **Authorize** and then click **Save**. You will now see a green “Authorized” label next to the G2G app.
![Authorized in CH](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte24871c9b7030760/690e467fc5fa98bc4def5e6b/img07_med.png?branch=integration)
