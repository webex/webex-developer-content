---
type: Excerpt
canonical_url: https://developer.webex.com/docs/experimenting-with-webhooks
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Get the ID of the Space'
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
