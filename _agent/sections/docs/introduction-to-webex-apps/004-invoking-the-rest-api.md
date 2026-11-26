---
type: Excerpt
canonical_url: https://developer.webex.com/docs/introduction-to-webex-apps
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Invoking the REST API
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/introduction-to-webex-apps). [Full Markdown](../../../../docs/introduction-to-webex-apps.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](001-prerequisites.md)

## Article introduction

This tutorial provides an introduction to Webex's extensibility.

---

In this introduction to the Webex REST API, you will use the interactive documentation to experience Webex programmability. The tutorial will then go through a few use-cases, and drill into the fundamentals of Webex Apps.

## Selected section

## Invoking the REST API

1. Navigate to **Full API Reference**>**Rooms** resource in the left-hand navigation pane.
1. In the left nav, click **POST Create a Room**.

1. Activate the documentation's **Try It** mode.

    ![Interactive mode](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte6306656e48af491/6202f44bc7047b4ac12ee476/step3-interactive-mode.png)

1. Edit the title of the Room and click **Run**.

    The right pane displays the request sent to the Webex API and the response received.
    ![Response](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd2c7233d84781dc8/6202f6e1c7047b4ac12ee47a/response.png)

    Note the request and response, because the request contains your access token, it is sent **on your behalf**.

1. Let’s examine the response. The `200 / OK` displayed in green is called the *HTTP status code* in the REST API terminology. It gives you instant feedback about the success or failure of your API call.

    The main HTTP status codes are '2xx' for success, '4xx' for client errors, and '5xx' for server errors. If you scroll down the page, the documentation shows various HTTP status code you may encounter.

1. Also, observe that the JSON response contains information about the newly created space such as its `id` property.

1. Now, open your Webex client and view the new room created by the API request.
    ![NewRoom](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2f0a1010e962df98/6202f7aeb7731b0ad7717b2d/new_room.png)

Next, let’s look at the potential of Webex extensibility.
