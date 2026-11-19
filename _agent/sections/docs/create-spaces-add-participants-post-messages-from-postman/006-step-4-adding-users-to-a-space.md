---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 4: Adding users to a space'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman). [Full Markdown](../../../../docs/create-spaces-add-participants-post-messages-from-postman.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Selected section

## Step 4: Adding users to a space

A collaboration space is persistent, as is the list of users who are members of that space. When you create a space, you are the only user in it. To collaborate, you must add other users to a space. 

Users are called *members* of a space. To add a user to a space, send an HTTP **POST** request to the `/memberships` resource. Include JSON-formatted membership information in the request's payload body, as shown below. Replace everything inside the quotes on the right side, including the curly brackets, with your values. The `{room_id}` will be what you copied and saved earlier and the `{new_user_email}` will be your personal email (or a bot email such as `toFrench@webex.bot`).

**Example JSON body**

```json
{
  "roomId" : "{room_id}",
  "personEmail" : "{new_user_email}",
  "isModerator" : false
}
```

>Note: This step requires a second email address. If you have a second email address available, you can create an additional account, or simply add a bot such as `toFrench@webex.bot`

1. Have the following information ready:
    * The email address of a second registered user
    * The `id` of the space created in Step 3
    * Your developer access token

1. In **Postman**, construct a REST **POST** request for the `/memberships` resource:
    * In the field marked *Enter request URL here* enter `https://webexapis.com/v1/memberships`
    * From the request method dropdown box, select **POST**
    * Select the **Headers** tab
    * Under **Key**, enter `Authorization`
    * Under **Value**, enter `Bearer` **followed by a space** and your access token
    * Add a second header where the name is `Content-Type` and value is `application/json`:
    ![Postman6](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltad56cf58a98948a2/61df51c6ec98266420c59176/postman6.png)
    * Click the **Body** tab, and select `raw`
    * In the large body text box, paste the JSON membership data shown above. Replace `{room_id}` with your new space's `id`, and replace `{new_user_email}` with the email address of the second user account. (Make sure to preserve the double quotes shown):
    ![Postman7](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb3efb508dd1b5b3b/61df52181757dc6aed2ae63d/postman7.png)

1. Click the **Send** button.

1. If the request is successful, the response displays JSON-formatted data that describes the new membership, including a unique `id` for the new member, and a `created` timestamp. In the Webex client, the space should now reflect that a new user has been added.

>Note: The Cisco Webex API documentation for managing Space Members is available at https://developer.webex.com/docs/api/v1/memberships
