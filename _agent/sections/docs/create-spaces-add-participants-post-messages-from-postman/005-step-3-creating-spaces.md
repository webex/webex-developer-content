---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 3: Creating Spaces'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman). [Full Markdown](../../../../docs/create-spaces-add-participants-post-messages-from-postman.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Selected section

## Step 3: Creating Spaces

Creating a new Webex space uses the same `/rooms` REST resource, but this time it uses the HTTP `POST` method. Also, it requires some extra information about the space, such as its title, represented as JSON data in the request body. For example:

```json
{
    "title": "Test Space"
}
```

1. In **Postman**, construct a REST **POST** request for the `/rooms` resource
    * In the field marked *Enter request URL here*, enter `https://webexapis.com/v1/rooms`
    * In the request method drop-down box, select **POST**
    * Select the **Headers** tab. Under **Key** enter `Authorization`
    * Under **Value**, enter `Bearer` followed by *a space character* and your access token
    * Click the row below to add a second header. For the Key name, enter `Content-Type`. For the Value, enter `application/json`:
    ![Postman3](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt3ab4e8df653b842c/61df51c58b16776549def2a2/postman3.png)
    * Select the **Body** tab (next to the Headers tab), and select the `raw` radio button. In the large body text box below, paste the JSON-formatted title of the space (the brackets and name-value pair shown above):
    ![Postman4](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt902e30a36b6aa6b4/61df51c514ef402247ceb71e/postman4.png)

1. Click the **Send** button to launch the request

1. If the request was successful, the response displays JSON-formatted data about the newly created space in the response, including its `id`. You can also see the new space in Webex:
    ![Postman5](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt471f885b27462fce/61df51c58aabbf6426b75d34/postman5.png)

1. Make a note of this space's **id**. You will use it in the following steps to add a participant and post a message to the space. You can use this <a href="https://developer.webex.com/posts/files/collab-webex-message/assets/notebox.html" target="\_blank">note-box page</a> as a temporary placeholder
