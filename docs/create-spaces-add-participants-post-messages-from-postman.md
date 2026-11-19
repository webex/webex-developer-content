---
type: Guide
title: Create Spaces, add participants, post messages from Postman
display_title: Create Spaces, add participants, post messages from Postman
canonical_url: https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/create-spaces-add-participants-post-messages-from-postman)

This tutorial describes ways to integrate with Webex from code to automate various tasks.

## Objectives

In this tutorial, you will learn to integrate with Webex from code to automate various tasks such as:

* Creating new persistent chat spaces
* Adding participants to existing spaces
* Posting messages to a space

By leveraging the same [Webex REST APIs](https://developer.webex.com/docs/getting-started), you will then be in good position to take it to the next stage to configure, monitor and secure your Webex organization, or create collaborative applications that create Enterprise workflows and enhance Customer experiences.


## Pre-requisites

You'll need a Webex account to take the steps of this tutorial.
If you don't have a Webex account yet, there's never been a better time to sign up. Simply [sign-up](https://cart.webex.com/sign-up), and create an account. Check your inbox for a 'You have a Webex account' message, and click the 'Create Password' verification link in it.

We will use the Postman REST client to create HTTP queries against the Webex API. After [downloading Postman](https://www.getpostman.com/apps) and installing on your laptop, we recommend you create a Postman account so that your work and collections can be saved to the cloud.


## Step 1: 'Webex for Developers' documentation

If you are new to Webex APIs, **Webex for Developers** is the place you'll want to start from: the portal exposes the reference documentation for the REST API, and the developer SDKs available to extend Webex.

1. Login at [Webex for Developers](https://developer.webex.com).

    > Note that you will not need to create a separate developer account. The same user account lets you access both Webex clients and 'Webex for Developers'

1. Once logged in, grab a temporary developer access token for your account by navigating to the [**Accounts and Authentication** section](https://developer.webex.com/docs/api/getting-started#accounts-and-authentication) of the **Getting Started** page:

    Copy your developer access token and save it in a safe place, as you'll be using the token in later steps of this tutorial:

    ![Developer Access Token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte72286f5ecee0087/61df5218dea73a236fc578ab/spark_access_token.png)

    > Note that your developer access token is provided for test purposes only - never use it in production. 
The token expires 12 hours after being generated, or upon logging out of 'Webex for Developers'. If your personal token is compromised, simply logout and sign in again on the developer portal to invalidate any previous tokens.

1. On that same page, scroll down and click the '+' icon next to **Full API Reference** in the left navigation panel to expand the API references. Check the various API resources entries in the table of contents:

    ![API Resources](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1f628059c6493986/61df51c51009c9654aca6b26/api-toc.png)

    These resources let you interact with spaces and receive notifications as users interact in Webex. The table below gives you a quick overview of some of the basic features offered by the Webex API resources:

    ![API Resources detailed](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbf77cde571168a12/61df51c5ef206c6c5e494d4d/api-resources.png)

1. Scroll down the API reference items and click on [Rooms](https://developer.webex.com/docs/api/v1/rooms) to access the documentation for the API used for managing spaces. The following is the URL we will use for accessing it from the REST client:
    ```shell
    https://webexapis.com/v1/rooms
    ```

    > *Note*: Webex *rooms* were renamed *spaces*. However, the Webex API still uses the `/rooms` resource, and room identifiers properties named `roomId`. Throughout these tutorials, you may see the 'Space' and 'Room' terms used interchangeably.

1. The 'Webex for Developers' API documentation is interactive: click the 'List Rooms' method on the [Rooms](https://developer.webex.com/docs/api/v1/rooms) page to view documentation for the API resource and try out sample requests. Make sure **Try It** mode is enabled to send HTTP requests and get instant responses from the Webex REST API right in your browser:

    ![Try It Mode](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt378df3c56a50969b/61df52182e109d6c649d470e/test-mode.png)

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
