---
type: Excerpt
canonical_url: https://developer.webex.com/docs/experimenting-with-webhooks
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Going further
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

## Going further

To learn more about the **Webhooks API**, check out [Webhooks](https://developer.webex.com/docs/webhooks) in the Webex documentation.

At the end of the day, webhooks are leverage by developers to create interactive chat bots. The labs below will drive you through the steps to build your first bots:

- Node.js tutorial: <a 

href="https://developer.cisco.com/learning/modules/spark-apps" target="\_blank">Creating Chatbots for Webex</a>
- Python tutorial: <a 

href="https://developer.cisco.com/learning/tracks/devnet-express-cloud-collab-it-pro/creating-spark-bots-itp/collab-spark-botl-itp/step/1" target="\_blank">Run a Webex bot locally</a>
