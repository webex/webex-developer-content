---
type: Guide
title: Guest to Guest Quickstart
display_title: Guest to Guest Quickstart
canonical_url: https://developer.webex.com/docs/guest-to-guest-quickstart
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/guest-to-guest-quickstart)

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

## Step 3: Request admin authorization

After successfully registering the Service App, you are taken to a page that contains a Client ID and Client Secret. This is also where you request admin authorization for the Service App.

1.  Copy & paste the **Client Secret** value into a notepad for later use. Do note, this client secret is only shown once.
2.  Click the ‘Request admin authorization’ button and keep the browser tab open.
3.  In the next section, you will act as the administrator to authorize the app.
![admin request](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt87f7bf69cbe9c17c/690e467f358d8e67bb4c8f8f/img05_med.png?branch=integration)

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

## Step 5: Retrieve the Access Token for the Service App

After you authorize the Service App as the admin in Control Hub, you can retrieve the access token. Do note that only one (1) G2G enabled Service App can be authorized per organization, which is determined by the `guest-meeting:rw` scope.

1.  Go back to the browser tab that displays the Client ID and Client Secret and refresh the page.
2.  In the ‘Org Authorizations’ section, select the test org name from the dropdown menu.
3.  Paste in the Client Secret value from your notepad in the field below, then click the ‘Generate tokens’ button.
![gen tokens](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt50db681f73ac8d37/690e467f6b2a06d853470151/img08_med.png?branch=integration)
4.  Copy & paste the `access_token` value in your notepad for later use. Token values are only shown one time.
![tokens](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt136301390398ea80/690e467ff60b0f1aafbc1fb6/img09_med.png?branch=integration)
## Step 6: Clone GitHub Repo to Install Python Demo App

Now that the Service App is ready, it’s time to clone the G2G demo app. Be sure you have Python and pip installed on your machine.

1.  Clone this repo from GitHub:
    `https://github.com/WebexSamples/webex-g2g-app.git`
2.  Open a command line window and navigate to the `webex-g2g-app` directory from the cloned repo.
3.  Install the dependencies:
    ```bash
    pip install -r requirements.txt
    ```
4.  Open the `webex-g2g-app` directory in a code editor.

## Step 7: Add the Access Token to the Demo App

1.  In your code editor, open the `.env.sample` file.
2.  Set the environment variable with the access token value you copied earlier by replacing the text in-between the quotes.
    ```bash
    WEBEX_ACCESS_TOKEN='Qdjfufn4uf45_example'
    ```
3.  Save the file.
4.  Rename the `.env.sample` file to `.env`

This is a good time to explore the `webex.py` and `app.py` files to get more familiarized with the app.

- The `webex.py` script essentially defines how Webex API methods are structured.
- The `app.py` script passes in API data to the various endpoints, such as [/meetings](https://developer.webex.com/meeting/docs/api/v1/meetings/create-a-meeting) for creating the meeting, [/guests/token](https://developer.webex.com/admin/docs/api/v1/guest-management/create-a-guest) for creating the guest identities, and [/meetings/join](https://developer.webex.com/meeting/docs/api/v1/meetings/join-a-meeting) for generating the meeting start & join link URLs.

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
