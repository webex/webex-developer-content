---
type: Guide
title: Experimenting with Webhooks
display_title: Experimenting with Webhooks
canonical_url: https://developer.webex.com/docs/experimenting-with-webhooks
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/experimenting-with-webhooks)

Webhooks allow your app to be notified via HTTP when a specific event occurs in Webex. An event could be triggered by a message being posted to a space, or a user joining or leaving a space, or a meeting that started or stopped. Events trigger in near real-time allowing your app and backend IT systems to stay in sync with new content and room activity.

---

You can think of webhooks as "reverse APIs" where the Webex cloud platform posts data to your application (instead of the other way around.) For example, you can register a webhook so that your application receives a notification every time a new message is posted in a particular Webex space.

![Webhooks diagram](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdbb3cc4d55c85298/6349e0791e79f1285f68717f/webhooks_img.png)



> **Info**
>
> Webhooks require a publicly reachable URL, where you application will be listening for inbound HTTP requests.



To make learning about creating and using webhooks easier, you'll use [ngrok](https://ngrok.com), an HTTP tunneling tool, running on your local system as a quick and easy way to inspect the contents of webhook messages without having to create and deploy a new backend service. 



> **Info**
>
> Of course, in a production situation, you would set up the webhook so that Webex sends the notification to an actual running application that you have coded (ngrok's main function is actually to forward such requests to a web app running on a local PC).  Today, we are just using ngrok by itself so that you can see how a webhook works without having to write an application first.



## Objectives

- Understand how Webex webhooks work
- Create a webhook
- View a webhook in action


## Prerequisites

To complete this tutorial you'll need the following:

- **A Webex account** &mdash; If you don't have a Webex account go to https://cart.webex.com/sign-up and follow the instructions to create one.
- **ngrok** &mdash; A public HTTP proxy service and client: https://ngrok.com/. 



## Step 1: Create a Space for Testing

For the purpose of this tutorial we'll capture events fired every time new messages are created in a space called "Marketing Campaign". You'll use the Webex app to create the space.

1. Open the Webex desktop app and press Ctrl+Shift+N or Cmd+Shift+N to open the new space page.
2. Give the space a name like ""Marketing Campaign", then click **Create**.


    ![Creating a test space](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltce2f9e122c40d608/623b9827549d685f55b5a3c0/create-space-in-webex.png)


## Step 2: Get the ID of the Space

As most Webex users have many spaces, we will use the **filter** parameter in our webhook request to restrict webhook notifications only for message events from the "Marketing Campaign" space. To do this we first need to determine the unique identifier (`id`) of the  space. We'll  use the **Try It** feature in the Webex interactive API reference to retrieve the names and IDs of all of the spaces where your user is a member, using the `/rooms` resource. 

**To obtain the ID of the new space**:

1. [Sign in](https://developer.webex.com/login) to the Developer Portal if you're not already signed in.
2. Open the [List rooms](https://developer.webex.com/docs/api/v1/rooms/list-rooms) API reference and make sure the **Use Personal Access Token** option is enabled.
3. Click **Run**.


    ![](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt260dca94a427e159/623b546b714afc639a7b23e0/try-it-list-rooms.png)

1. Scroll down to view the results and locate the "Marketing Campaign" item in the JSON results.


    ![](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb13d31c2c5b905b8/623b546bbe82216394d3eb94/try-it-results-list-rooms.png)

1. Copy the value of the `id` field to your clipboard.


## Step 3: Setup ngrok to capture web requests

Next you'll download and start ngrok on your local system and obtain its public HTTPS URL. You'll provide this URL when you create the webhook that will listen for events.

**To set up ngrok service and retrieve its unique URL:**

1. [Download the ngrok client](https://ngrok.com/download) and unzip it. (It's not necessary to sign up to use ngrok.)
2. Open a terminal window and navigate to the download directory.
3. Launch `ngrok` to listen for HTTP requests on port 5000:


- **Mac/Linux**: `./ngrok http 5000`
- **Windows**: `ngrok http 5000`


    When ngrok starts up it will display some information about the service, including its public HTTPS URL:

    ![ngrok screenshot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt87bbbb380ff73470/623a6654159fc76504c175c3/ngrokscreenshot.png)

1. Copy and save this HTTPS URL for use in the next steps.
2. Open a web browser and browse to `http://localhost:4040` to view the ngrok request inspector:


    ![ngrok screenshot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6153691a0c221034/623a6654483e2c64fe287a7c/ngrokinspector.png)

    This is where you will observe JSON payloads for each webhook event later in the tutorial.

## Step 4: Register a new webhook

To begin receiving events you need to register a webhook with Webex. To do this you make an HTTP **POST** to the  `/webhooks` resource URL, passing it information about the webhook, including the URL that should be notified when the event occurs. You also specify the type of API resource you want the webhook to monitor ('messages'), the kind of event ('created'), and a filter to limit events for the room ID you obtained in the previous step. For details about the types of resources, events, and filters available for webhooks, see the [Filtering Webhooks](https://developer.webex.com/docs/webhooks#filtering-webhooks).

**To register a new webhook**:

1. Open the [Create a Webhook](https://developer.webex.com/docs/api/v1/webhooks/create-a-webhook) API reference and make sure the **Use Personal Access Token** option is enabled. 
2. In the **Body** section of the request form, fill out the fields with the following information, replacing **&lt;ngrok-url>** and **&lt;room-ID>** with the ngrok URL and room ID obtained in steps 2 and 3.


    | Input field | Value                   |
    | ----------- | ----------------------- |
    | name        | **Messages webhook**    |
    | targetURL   | **&lt;ngrok-url>**      |
    | resource    | **messages**            |
    | event       | **created**             |
    | filter      | **roomId=&lt;room-ID>** |

1. Click **Run** to create the new webhook. 


    A successful HTTP response contains a JSON representation of the newly created webhook.

	![Webhook Response](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf1ccd875c9efeea9/623b946b5fa15f0a668450e6/webhookresponse.png)

Next you'll observe JSON payloads being send to your ngrok endpoint when new messages are created in the Marketing Campaign space.

## Step 5: Observe the Webhook in Action

Let's put it all together so we can see the webhook in action. Any new message that is added to the Marketing Campaign space will trigger the webhook, which will cause Webex to send a notification to the target ngrok URL. Each notification is a JSON object that includes the ID of the new message, and other information about what caused the notification. See [Handling Requests from Webex](https://developer.webex.com/docs/webhooks#handling-requests-from-webex) for details about all the fields returned by the webhook.

**To view webhook events:**

1. Open the Webex app and post a message in the "Marketing Campaign" space. 


    ![Sending a message to space](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9310ff688a78a093/623b8ceb549d685f55b5a3a0/send-message-webex.png)

1. In your browser open the ngrok inspector URL at http://localhost:4040 to see the Webex webhook notification message details, which will look like the following:


    ![ngrok screenshot](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte1acd9c1ad2a70e0/623a6654e6c8cf4de6f6dace/messagedetails.png)

    

> **Info**
>
> The `502 Bad Gateway` message is expected, as ngrok is not configured to point to an actual listening app



	Here's an example JSON body formatted for easier reading:

    ```json  
    {
      "id":"Y2lzY29zcGFyazovL3VzL1dFQkhPT0svZjRlNjA1NjAtNjYwMi00ZmIwLWEyNWEtOTQ5ODgxNjA5NDk3",
      "name":"Guild Chat to http://requestb.in/1jw0w3x1",
      "resource":"messages",
      "event":"created",
      "filter":"roomId=Y2lzY29zcGFyazovL3VzL1JPT00vY2RlMWRkNDAtMmYwZC0xMWU1LWJhOWMtN2I2NTU2ZDIyMDdi",
      "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
      "createdBy": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xZjdkZTVjYi04NTYxLTQ2NzEtYmMwMy1iYzk3NDMxNDQ0MmQ",
      "appId": "Y2lzY29zcGFyazovL3VzL0FQUExJQ0FUSU9OL0MyNzljYjMwYzAyOTE4MGJiNGJkYWViYjA2MWI3OTY1Y2RhMzliNjAyOTdjODUwM2YyNjZhYmY2NmM5OTllYzFm",
      "ownedBy": "creator",
      "status": "active",
      "actorId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xZjdkZTVjYi04NTYxLTQ2NzEtYmMwMy1iYzk3NDMxNDQ0MmQ",
      "data":{
        "id":"Y2lzY29zcGFyazovL3VzL01FU1NBR0UvMzIzZWUyZjAtOWFhZC0xMWU1LTg1YmYtMWRhZjhkNDJlZjlj",
        "roomId":"Y2lzY29zcGFyazovL3VzL1JPT00vY2RlMWRkNDAtMmYwZC0xMWU1LWJhOWMtN2I2NTU2ZDIyMDdi",
        "personId":"Y2lzY29zcGFyazovL3VzL1BFT1BMRS9lM2EyNjA4OC1hNmRiLTQxZjgtOTliMC1hNTEyMzkyYzAwOTg",
        "personEmail":"person@example.com",
        "created":"2015-12-04T17:33:56.767Z"
      }
    }
    ```

	The JSON object's `data` field contains a JSON representation of the message resource that triggered the webhook, including the ID of the message, the room ID, as well as the ID and email of the person who sent the message. To get the actual message text, you make another request to the `GET /messages` API, passing the ID of the message as parameter.

1. Copy the value of the `data` object's `id` field to your clipboard, which is the ID of the newly created message. 


**To get the message text:**

To see the new message in our webhook request, we'll make a request to the [Get Message Details](https://developer.webex.com/docs/api/v1/messages/get-message-details) API.

1. Open the [Get Message Details](https://developer.webex.com/docs/api/v1/messages/get-message-details) API reference page.
2. Click on the `messageId` URL fragment and paste in the message ID you obtained in the previous steps.


    ![Adding message ID to request URL](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1a29cddfa6677a3a/623b90ef714afc639a7b24d6/get-message-details.png)

1. Click **Run**. The message details are displayed in the **Results** area.


    ![Response](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta3a7813ca25f6ba4/623b91d3714afc639a7b24da/message-contents.png)

## Going further

To learn more about the **Webhooks API**, check out [Webhooks](https://developer.webex.com/docs/webhooks) in the Webex documentation.

At the end of the day, webhooks are leverage by developers to create interactive chat bots. The labs below will drive you through the steps to build your first bots:

- Node.js tutorial: <a 

href="https://developer.cisco.com/learning/modules/spark-apps" target="\_blank">Creating Chatbots for Webex</a>
- Python tutorial: <a 

href="https://developer.cisco.com/learning/tracks/devnet-express-cloud-collab-it-pro/creating-spark-bots-itp/collab-spark-botl-itp/step/1" target="\_blank">Run a Webex bot locally</a>
