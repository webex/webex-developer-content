---
type: Article
title: Creating a Meeting Scheduler as a Webex Service App
canonical_url: https://developer.webex.com/blog/creating-a-meeting-scheduler-as-a-webex-service-app
content_type: blog
date: '2024-11-20'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/creating-a-meeting-scheduler-as-a-webex-service-app)

[Webex Service Apps](https://developer.webex.com/docs/service-apps) are machine accounts that can access the Webex APIs on behalf of an organization instead of individual users. This makes them optimal for running mission-critical integrations and long-term tasks for a Webex org. Many popular Webex Service Apps are administrative integrations, such as automated [provisioning](https://developer.webex.com/docs/webex-calling-provisioning-apis) and [active reporting](https://developer.webex.com/blog/exploring-the-webex-calling-reports-and-analytics-apis) use cases. They are also commonly used for [Compliance Officer](https://developer.webex.com/docs/compliance) integrations that continuously maintain regulatory policies, eDiscovery, and other security tasks inside of Webex Messaging, Meetings, and Calling.

Another great way some of our largest enterprise customers are leveraging Service Apps is to automate the scheduling of Webex meetings for anyone within an organization. For example, a Human Resources Management (HRM) tool that streamlines the scheduling of job interview and onboarding sessions in Webex Meetings. With a Service App, these meetings are scheduled on behalf of the organization, which eliminates the need for a specific administrator to authorize the HRM integration on their own account to schedule meetings across the organization. This scenario is also an ideal fit for Service Apps because the meeting scheduler integration is a critical component of the HRM tool and used on a full-time basis.

### Getting Started with the Demo

To get familiarized with how the basic parts come together, this blog will take you through a step-by-step demo for creating a Webex Service App meeting scheduler using a sample Python application. When trying these steps on your own, you will need to have few things to start:

1. Admin access to Webex (Control Hub). You can get this with a [Webex Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide). 
1. Make a couple test user accounts in the sandbox org that the Service App will schedule meetings for. The easiest way is to [manually add users](https://help.webex.com/en-us/article/v71ztb/Add-Users-Manually-in-Control-Hub).
1. [Python 3.x](https://www.python.org/downloads/) installed on your machine.

<br/>

### Step 1: Create a Webex Service App

To start, a Service App needs to be created in the developer portal. Have the credentials ready your sandbox admin and test users:

1. Login to [developer.webex.com]() using credentials from one of your (non-administrator) sandbox test users.
1. Up on the top right corner of the page, click your avatar and then select **My Webex Apps**.
1. On the **Create a New App** page, find the **Service App** card and click **Create a Service App**:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8c8556f2fbf45d59/service-apps-meeting-scheduler-blog-2.png)
1. Fill out the webform to register a new service app. Pay extra attention to the **scopes** section to ensure the app has admin permission to schedule meetings:
    - **App Name:** meeting-scheduler-demo
    - **Icon:** *Select any color icon.*
    - **Description:** “Demo app only”
    - **Contact Email**: Use the email from the test user login.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbafba8a0e95dc524/service-apps-meeting-scheduler-blog-3.png)
    - **Scopes**: For this demo app, we only need to select the `meeting:admin_schedule_write` scope. In a real-world scenario, the meeting scheduler app would likely require the `read` scope and potentially other scopes.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt516456f6a685c9a8/service-apps-meeting-scheduler-blog-4.png)
1. Click the **Add Service App** button to finish registration:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte882db486a251276/service-apps-meeting-scheduler-blog-5.png)

### Step 2: Service App Authorization

After successfully registering the Service App, you are taken to a page that contains a **Client ID** and **Client Secret**, which are required for all Service Apps. This is also where you request an admin to authorize the Service App in Control Hub:

1. Copy &amp; paste the **Client ID** and **Client Secret** values into a notepad for later use. Do note, this client secret is only shown once.
1. Click **Request admin authorization**. Keep this tab open, as we will be going back to it.
    For this demo, we also need to act as the administrator inside Control Hub to authorize the Service App that was just created:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6c9f5b9117f777b0/service-apps-meeting-scheduler-blog-6.png)
1. Open an incognito browser tab and login to [admin.webex.com](https://admin.webex.com/) using the administrator credentials for your sandbox.
1. On the left navigation pane in Control Hub, look under the **Management** section and select **Apps**.
1. On top of the **Apps** page, select the **Service Apps** tab.  
1. Click the **meeting-scheduler-demo** app, which will open the details on the far right. The details include the description and scopes that were entered when the Service App was created.
1. Slide the thumb button to enable **Authorize** then click **Save** at the bottom.

<br/>

### Step 3: Retrieve the Access and the Refresh Token

After the admin authorizes the Service App registration, the test user can now retrieve the access tokens for the APIs. The tokens are used like a traditional integration and the same token expiration policies apply - 14 days for the access token and 90 days for the refresh token:

1. Refresh the tab that displayed the **Client ID** and **Client Secret**.
1. In the **Org Authorizations** section, select the name of your sandbox org from the dropdown menu.
1. Paste in the **Client Secret** value from your notepad in the field below, then click **Generate tokens**.
1. Copy &amp; paste the `refresh_token`and `access_token` values in your notepad for later use in the demo app. *Both values are only shown once.*

<br/>

### Step 4: Install and Configure the Sample Python App

Now that the access and refresh tokens are ready, we can download the sample app and using a code editor, insert the tokens into the Python code and configure the meeting. When complete, the app will automatically schedule a meeting for the next day with your test user host and no attendees:

1. Download [simple_service_app](https://github.com/WebexSamples/simple_service_app/archive/refs/heads/main.zip) from GitHub and unzip the file to install it.
1. Open a command line window and navigate to the `simple_service_app-main` directory that was just installed. Keep this window open.
    - `cd simple_service_app-main`
1. Now open the `serviceapp.py` file in an external code editor (such as VS Code):
    1. Go to [line 25](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L25) of the code and replace the text with the `clientID` value from your notepad.
    1. On [line 26](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L26), replace the text with the `secretID` value from your notepad.
    1. On [line 27](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L27), replace the text with the `access_token` value from your notepad.
    1. On [line 28](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L28), replace the text with the `refresh_token` value from your notepad.
    1. Scroll to [line 67](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L67), after `'title':` replace the text and give your meeting a unique name.
    1. On [line 70](https://github.com/WebexSamples/simple_service_app/blob/main/serviceapp.py#L70), after `'hostEmail':` replace the text with the email address of a test account from your sandbox, which does not necessarily have to be the same account that created the Service App. This will tell the Service App to schedule the meeting with your test user as the host.
    1. Save the `serviceapp.py` file.

<br/>

### Step 5: Run the Sample Service App

With all the Service App components added to the Python code, the sample app is now ready to be initialized:

1. Go back to the command line window in the `simple_service_app-main` directory.
1. Install [Requests](https://pypi.org/project/requests/) library for Python (if needed) with the following command, `pip install requests`.
1. Launch the `serviceapp.py` file from that location with this command, `python3 serviceapp.py`.

A successful launch will return a `statusCode 200` along with the newly created meeting details in JSON format:

```bash
{'id': '7f36776aa9034d6091ef00dcee83ced2','meetingNumber': '26607444195','title': 'My Service App Meeting,'password':…,…}
```

### Step 6: Verify the Scheduled Meeting

You can quickly confirm that the Service App scheduled the meeting for the test user with one more API call.

1. Go back to the browser and login to developer.webex.com*as the test user that is the meeting host*.
1. Navigate to the [List Meetings API](https://developer.webex.com/docs/api/v1/meetings/list-meetings) reference page.
1. Make an API call to list meetings for the test user by clicking the orange **Run** button (scroll down, along the right side).

The response should return a `200/OK` and provide the meeting information that was scheduled by the Service App for the test user:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf4b32e2c666443d/service-apps-meeting-scheduler-blog-7.png)

### Conclusion

As this demo showed, Webex Service Apps can act as a Webex administrator to schedule meetings for users within an organization. There are countless ways automated meeting scheduling functionality can be incorporated into larger organizational applications, such as virtual training, remote consultations, and wellness programs. With Service Apps, they can safely run on a long-term basis independent of any individual users.

### Need Some Help? No Problem!

We are happy to provide you with support for any of the features in this article. If you need help or have any questions, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Until next time, happy developing!
