---
type: Excerpt
canonical_url: https://developer.webex.com/docs/experimenting-with-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 5: Observe the Webhook in Action'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/experimenting-with-webhooks). [Full Markdown](../../../../docs/experimenting-with-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md) [Step 3: Setup ngrok to capture web requests](005-step-3-setup-ngrok-to-capture-web-requests.md)

## Article introduction

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

## Selected section

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
