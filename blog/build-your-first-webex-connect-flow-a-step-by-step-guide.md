---
type: Article
title: 'Build your first Webex Connect Flow: A Step-by-Step Guide'
canonical_url: https://developer.webex.com/blog/build-your-first-webex-connect-flow-a-step-by-step-guide
content_type: blog
date: '2024-08-01'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/build-your-first-webex-connect-flow-a-step-by-step-guide)

Webex Connect is a powerful Communications Platform as a Service (CPaaS) built to enable enterprises to automate digital interactions at scale. Developers can integrate channels such as SMS and WhatsApp, technologies such as AI and payments, and systems into applications.

In addition to its powerful API capabilities, Webex Connect helps developers to work quicker and smarter through the Flow Builder, which is used to build, configure, deploy, and iterate workflows that automate communication processes across the customer journey. By embracing the Flow Builder, developers can expedite the creation of communication-powered solutions for the business units they serve.

This blog will walk you through creating, configuring, testing, and troubleshooting your first Webex Connect flow using the Flow Builder.

Before we dive in, ensure you have the following:

- A Webex Connect account - you can create a Webex Connect Developer Sandbox account via the [Webex CPaaS Developer Hub](https://cpaas.webex.com/products/webex-connect/developer-hub).
- An HTML5 capable web browser such as Firefox, Chrome, Safari, or Edge.
- Postman, an HTTP/REST API test client, for API interaction.

<br/>

### What We’ll Build

Our objective is to create a flow that notifies a patient of their appointment and allows them to respond via SMS. To do this, first, we need to access the Webex Connect Flow Builder.

### Get started with the Flow Builder

<br/>

#### Navigate to the Service Dashboard

At the highest level, Webex Connect lets you organize flows by projects called Services. Typically, these would be created for each of your application customer interactions and journeys.

For now, let's just access the auto-created default service:

1. From the left-side navigation bar, click on the Services icon:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltef57be2b63b3a062/webex-connect---how-to-build-your-first-flow-3.png)
1. Choose the default "My First Service"
    This should take you to the service Dashboard, which provides an overview of your service's activity and configuration, including analytics on recent traffic activity, access to the REST API docs/tools, and the Flow Builder itself.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt40b917fe1b9508d5/webex-connect---how-to-build-your-first-flow-4.png)

#### Start Building a Flow

<br/>

1. Select the **Flows** tab, then go ahead and click **Create flow**. Give the flow a name.
    For this lab, let's create our flow using the "Appointment" template:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9784b622eef15330/webex-connect---how-to-build-your-first-flow-5.png)
    This will open up the Flow Builder, which will automatically open the **Configure Webhook** property page.
1. Our flow will be triggered by an incoming [webhook](https://developers.imiconnect.io/reference/custom-event-v2) - i.e., an `HTTP POST` with some JSON-formatted initial data. You can view your flow's auto-generated webhook URL here:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76a99659dde0d40a/webex-connect---how-to-build-your-first-flow-6.png)
    Webhooks are a very common way for applications to send events and data to each other; for example, a health clinic's patient system could send a batch of webhooks to this flow each day based on a query of all patients booked for appointments the next day.
    Go ahead and give your webhook a name - can be anything, perhaps "Appointment Webhook"
1. The trigger webhook will need to deliver actionable data from an application to the flow, such as the recipients information.
    Define the expected JSON contents (just the keys) by pasting this sample webhook payload into the **PROVIDE SAMPLE INPUT** area:

    ```json
    {
      "Phone": "",
      "Name": "",
      "Appt": ""
    }
    ```

1. Click **PARSE**.
    If the data is parsed correctly, it should look like this:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7c0f0f60f2f268ee/webex-connect---how-to-build-your-first-flow-7.png)
1. That's all the trigger configuration needed for now. Go ahead and click **Save**, which should bring you to the Flow Builder main screen.

You can see that a fairly complete flow has been automatically created, including event, data and logic nodes and logical interconnections needed to orchestrate them. The gist of what this flow does and how it works can be gleaned with just a quick inspection.

Feel free to play around in the Flow Builder for a bit: check out the **Utilities**/**Channels**/**Integrations** tabs, try out the bottom toolbar options, peek into some of the nodes (double-click), etc.

Note: If you make a change (e.g., dragging-dropping a new node onto the canvas) and can't manage to undo it (i.e., with Ctrl+Z), you can always delete the flow and recreate it from the template.

#### Send the Initial SMS

We've already configured the flow's triggering webhook (we'll learn how to test it a bit later), the next step in the sequence will be to send the initial notification SMS to the patient based on the webhook's data variables:

1. Double-click on the **Send SMS** node to open it and view the configuration page.
1. Delete the place-holder contents of the **Destination** field.
    Replace it by opening the *Start* collection on the right side and clicking **inboundWebhook.Phone**:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7de762413b6e617b/webex-connect---how-to-build-your-first-flow-8.png)
1. In the **FROM NUMBER** field, select the (default, only) Sender ID:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7d2e3533afc87b3e/webex-connect---how-to-build-your-first-flow-9.png)
    This is a phone number associated with your Webex Connect Service - i.e., the 'Caller ID' the patient will see for the SMS.
1. In the **MESSAGE** field, delete `$(name)` and `$(dateTime)` from the message text, and replace with `inboundWebhook.Name` and `inboundWebhook.Appt`:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt75aaf4b1b69811fa/webex-connect---how-to-build-your-first-flow-10.gif)
1. You can now **Save** the configuration.

#### Receive the Patient Response

Once the initial reminder SMS has been sent to the patient, the flow will need to await the patient's response (if any!):

1. Open the **Receive** node configuration.
1. In the **Receive SMS** section, select the inbound **NUMBER** where we are expecting the patient's response to arrive (this would be the same number the initial SMS was sent from).
1. Choose ***** for the **KEYWORD**.
1. Replace the **FROM NUMBER** with **inboundWebhook.Phone** (under the *Start* variables), i.e., the patient's phone number.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt82ffdb5456243b95/webex-connect---how-to-build-your-first-flow-11.png)
    

> **Info**
>
> The **MAXTIMEOUT** value of **600** means that the flow will wait a maximum of 600 seconds (10 minutes) for the patient's reply.


1. Go ahead and *Save*.

<br/>

#### Check the Response

Sending the initial response will have a number of results:

- The user replies with 'A' to keep the appointment.
- The user replies with 'B' to cancel the appointment.
- The user replies with something unexpected.
- The user never replies.

The *Branch* node can make *if/then/else* decisions about which branch of the flow to follow next:

1. Open the "Check User Response" branch node config.
1. We don't actually need to configure anything here (the template provided the current values), but by inspecting the *Confirm* and *Cancel* conditions, we can see that the node is checking if the received message content output variable from the previous receive node `($(n11.receive.message))` "Equals" **A** or **B**.
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3a2661c8e7ffce01/webex-connect---how-to-build-your-first-flow-12.png)

A default "None of the Above" condition is also there too.

#### Report on Progress

As this flow could actually take a number of minutes to reach its final end point, it might be nice if we could monitor its progress.

This is possible by using the *HTTP* node type to send an *outbound* message to an external service – here’s a handy, free hook bin service: [Webhook.site](https://webhook.site/)

In a real flow, the external service would be a reporting, analytics or dashboard application that would receive the notification + data, then update its state tracking on the appointment notification request. However, for our purposes, we'll just use the hook bin to accept the message so we can inspect the HTTP/JSON contents of the outbound webhook:

1. Open a new browser tab and navigate to: [Webhook.site](https://webhook.site/).
    (Feel free to use another hook/request bin.)
    It should display an auto-generated unique URL where webhooks can be directed:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf62b010371d072c2/webex-connect---how-to-build-your-first-flow-13.png)
    Copy this to your clipboard, and/or keep this tab open. **Important**: You must also select the option to enable [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing):
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc2332bdf4cdc9d05/webex-connect---how-to-build-your-first-flow-14.png)
1. In the Flow Builder, open the top-most **HTTP** node (the one on the "Confirm" branch.)
1. Change the **METHOD** to **POST**.
1. Paste your hook bin's unique URL into the **ENDPOINT URL** field.
1. For the **BODY** we'll just relay all the data from the original triggering webhook, *PLUS* a *Status*: Confirmed field indicating how the interaction with the patient is proceeding:

    ```json
    {
      "Phone": "$(n2.inboundWebhook.Phone)",
      "Name": "$(n2.inboundWebhook.Name)",
      "Appt": "$(n2.inboundWebhook.Appt)",
      "Status": "Confirmed"
    }
    ```

    

> **Info**
>
> We're getting the run-time data values from the **Start** variables list on the right-hand side.


1. Open the *Node Outcomes* group in the lower right:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt11e0a4a9123e6b8a/webex-connect---how-to-build-your-first-flow-15.png)
    Notice that an *HTTP* node type has two defined outcomes: `onerror` and `oncomplete`. This results in corresponding branches in the Flow Builder that will need to be handled (already in place from the template):
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd9fe7df88d030fe2/webex-connect---how-to-build-your-first-flow-16.png)
1. Go ahead and **Save** this node.
1. Repeat the steps above for the *HTTP* node on the *Cancel* branch, but this time sending `Status: Cancelled`:

    ```json
    {
      "Phone": "$(n2.inboundWebhook.Phone)",
      "Name": "$(n2.inboundWebhook.Name)",
      "Appt": "$(n2.inboundWebhook.Appt)",
      "Status": "Cancelled"
    }
    ```

#### Final Configurations

The five remaining nodes that we haven't configured yet are all SMS nodes:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7f997c317bb551f0/webex-connect---how-to-build-your-first-flow-17.png)

Configure all of these with the same **DESTINATION** and **FROM NUMBER** values as the initial SMS node:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3e75fe7fa2ac9e26/webex-connect---how-to-build-your-first-flow-18.png)

#### Publish Live

The flow is complete and should now be ready to publish!

1. Since we're in dev/test mode, click on the *Settings* gear icon in the upper right.
    Under **General / Advanced** settings, enable *Descriptive logs*.
    This will give us detailed information about the inputs, outputs and any errors for each flow node, which will help greatly with any needed troubleshooting!

    

> **Info**
>
> Once your flow is complete, tested and stable you will likely want to disable *Descriptive logs* to avoid having any sensitive enterprise or customer data written to the logs.


1. From the Flow Builder overview, click on **Save** in the top-right corner:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5bdd8cb57085568f/webex-connect---how-to-build-your-first-flow-19.png)
    During the save process, the system checks that the flow is valid and correctly configured. If there is a problem, you may see an error/warning message in the top-right:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt584cbd83c3366a81/webex-connect---how-to-build-your-first-flow-20.png)
    Clicking on the error will select the offending node, allowing you to correct its configuration and re-save.
1. Finally, click **Make Live**:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0ebd9630fc1b0ff3/webex-connect---how-to-build-your-first-flow-21.png)
    Entering a comment is optional, but can be useful - e.g., for versioning.

#### Test the Flow

With the flow live and ready to interact with enterprise systems and patients/customers, it's time to give it a test run!

If you recall, the first thing we did after creating the flow was to configure the triggering *inbound* Webhook:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd4650f6bffe16a89/webex-connect---how-to-build-your-first-flow-22.png)

Since we don't have an actual enterprise back-end system programmed to send a real webhook, we need a way to send the webhook message ourselves, for this we will use [Postman](https://www.postman.com/).



> **Info**
>
> You can also use [Curl](https://curl.se/) from the terminal, or almost any other HTTP tool to make the webhook *HTTP POST.*



Let's configure and send the *HTTP POST* request needed to trigger our flow:

1. Open Postman, and click the "+" button to create a new request.
1. Select **POST** from the method dropdown.
1. In the URL field, paste in your triggering webook's URL.
    You can retrieve this by going back to the Flow Builder by double-clicking the trigger **Webhooknode** and grabbing the *WEBHOOK URL*:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt76a99659dde0d40a/webex-connect---how-to-build-your-first-flow-6.png)
1. Select the **Body** tab.
    Choose **raw** type, and then **JSON** format from the dropdown.
1. For the request body itself, copy the sample input *JSON BODY* from your trigger *Webhook* node and paste, inserting some test data (you can use your mobile number for *Phone*, being sure to include the country code but not a "+", e.g "1" for the US or 44 for the UK):

    ```json
    {
      "Phone": "14055551212",
      "Name": "Jane Doe",
      "Appt": "March 4, 2022"
    }
    ```

    The final request should look like this:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltcdf7e5f4da8f316f/webex-connect---how-to-build-your-first-flow-23.png)
1. Now you can click Send to fire off the webhook.

#### Verifying and Troubleshooting

If all went well, a number of things should happen:

1. You should receive an appointment reminder SMS on your mobile phone.
1. Replying with "A" or "B" should result in the appropriate acknowledgement SMS message.
1. After the patient reply step, checking your hook bin web page you should see an *HTTP POST* message has arrived, containing the JSON "progress" message configured in the flow's *HTTP* node.
1. If after sending the webhook something unexpected happens (including nothing!), you can click on the *Debug* "bug" icon to examine the logs and drill into specific node operations for errors and clues:
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4afba31c5bbcecb2/webex-connect---how-to-build-your-first-flow-24.png)

### Congratulations and Next Steps!

Congratulations on completing your first Webex Connect flow!

Hopefully this walkthrough has showcased how the Flow Builder enables enterprise developers to work in a more efficient way to accelerate IT roadmaps and better meet the needs of their organizations.

This is just the beginning—continue exploring additional templates, channels, nodes, use cases, and API capabilities. Consider requesting full access to unlock more enterprise features and even book a demo to deepen your understanding of Webex Connect.

In this blog, we not only introduced you to the basics of Webex Connect but also equipped you with the knowledge to build more complex flows and integrations.

For more Developer Resources, you can visit the [Webex CPaaS Developer Hub](https://cpaas.webex.com/products/webex-connect/developer-hub).
