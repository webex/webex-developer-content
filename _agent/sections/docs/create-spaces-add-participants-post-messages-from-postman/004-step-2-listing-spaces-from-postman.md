---
type: Excerpt
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- 'Step 2: Listing spaces from Postman'
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman). [Full Markdown](../../../../docs/create-spaces-add-participants-post-messages-from-postman.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Selected section

## Step 2: Listing spaces from Postman

Webex users rely on persistent **spaces** to collaborate with other users by instant message, voice, video, and file sharing.

To begin with, we will use Postman to fetch the list of spaces to which your user belongs, by sending a query to the `/rooms` resource:

1. Launch **Postman** (click **Reset** if necessary to clear out any previous info)

1. In **Postman**, construct a REST **GET** request for the `/rooms` resource
    * In the field marked *Enter request URL*, enter `https://webexapis.com/v1/rooms`
    * Select **GET** in the HTTP method drop-down menu
    * Click the **Headers** tab
    * Under **Key** enter `Authorization`
    * In the same row, under **Value** enter `Bearer` **followed by a space** and your access token
    ![Postman1](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4bff242afba8a5b1/61df51c5dbd06039fdcf86cb/postman1.png)

1. Click the **Send** button

1. If the request is successful, the response displays JSON-formatted data corresponding to your Webex spaces. Each space has an `id` name-value pair:
    ![Postman2](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltabfa99172117a2f3/61df51c51757dc6aed2ae635/postman2.png)
