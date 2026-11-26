---
type: Excerpt
canonical_url: https://developer.webex.com/docs/experimenting-with-webhooks
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Setup ngrok to capture web requests'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/experimenting-with-webhooks). [Full Markdown](../../../../docs/experimenting-with-webhooks.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

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
