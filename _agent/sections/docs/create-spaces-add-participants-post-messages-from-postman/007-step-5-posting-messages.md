---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 5: Posting messages'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman). [Full Markdown](../../../../docs/create-spaces-add-participants-post-messages-from-postman.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Selected section

## Step 5: Posting messages

As the final step, we will post a new message to a space using the Webex API's `/messages` resource using HTTP **POST**.

>Note: For more details about the /messages API Resource, check: https://developer.webex.com/docs/api/v1/messages

In the request payload's body, include some JSON-formatted data that represents the text of the new message:

```json
{
  "roomId": "{room_id}",
  "text": "Hello World!"
}
```

1. Have the following information ready:
    * The `id` of the Webex space created in Step 3
    * Your Webex access token

2. In **Postman**, construct a REST **POST** request for the `/messages` resource:
    * In the field marked *Enter request URL*, put the URL for the Webex API `/messages` resource: https://webexapis.com/v1/messages
    * From the request method drop-down box, make sure **POST** is selected
    * Select the **Headers** tab, under **Key**, enter `Authorization`
    * Under **Value**, enter `Bearer` followed by *a space character* and your access token
    * Add a second header whose name is `Content-Type` and whose value is `application/json`
    ![Postman8](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd85fe89a4bb07d79/61df5218bf9cb8387cc1e589/postman8.png)
    * Select the **Body** tab, and make sure `raw` is selected. In the large body text box, paste the JSON data shown above. Be sure to replace `{room_id}` with the space `id` saved in step 3 (but make sure the quotes remain as shown):
    ![Postman9](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltffcf070b39010f77/61df52188b16776549def2aa/postman9.png)

3. Click the **Send** button to launch the request

4. If the request is successful, the response should display JSON-formatted data describing the new message, such as the message's unique `id`, and a `created` timestamp

5. Open your Webex client, and check that the space displays the new message!

### Markdown formatted messages

Using the Markdown markup syntax, Webex clients can render rich text across all platforms - mobile, desktop and web.

Visit https://developer.webex.com/docs/basics#formatting-messages to check out the possibilities offered. By replacing the "text" property in the previous JSON body to "markdown", you will be able to post enriched messages: bold, italic, links, ordered and unordered lists, block quotes, in-line code, code blocks, and @mentions:

```json
{
  "roomId": "{room_id}",
  "markdown": "This API is really **awesome**\n\n>You bet!"
}
```

### Going further

In this tutorial, we only scratched the surface of the Postman REST client capabilities. We encourage you to explore code generation and [hidden treasures with Postman](https://www.getpostman.com/docs/postman/collections/creating_collections)!

If you want to give these a try, follow the [instructions on GitHub](https://github.com/CiscoDevNet/postman-ciscospark) to import a scripted Postman collection for Webex, and access the full set of Webex APIs in a single location:

![Scripted Collection](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3bd5a85d7a1a5ffc/61df5218ec98266420c5917e/postman-collection.png)
