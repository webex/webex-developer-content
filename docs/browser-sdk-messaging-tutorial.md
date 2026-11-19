---
type: Guide
title: Browser SDK Messaging Quick Start
display_title: Browser SDK Messaging Quick Start
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
content_type: documentation
product_group:
- webex-suite
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/browser-sdk-messaging-tutorial)

## Browser SDK Messaging Sample App

This tutorial shows how to use the [Webex Browser SDK](https://developer.webex.com/docs/sdks/browser) to do the following:

* List rooms (spaces) you belong to
* Create and delete rooms
* Send a message to a room
* Add members to a room
* Listen for newly created or deleted messages in a room

![App overview](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte8c294887b72ae5a/63485494e72880168de5e4d3/app-overview.png)

## Project Starter Files

You can obtain starter and completed project files on [GitHub](https://github.com/WebexSamples/browser-sdk-demo).

* **index.js** -- Contains code to initialize the Webex SDK with your personal access token (see [Getting your personal access token](https://developer.webex.com/docs/browser-sdk-messaging-tutorial#getting-your-personal-access-token)) and defines a simple logging function.
* **index.html** -- Loads the Webex SDK and application code, and provides a basic UI with buttons to invoke various SDK methods. You will create the functions defined for each button's `onclick` attribute.

## Getting your Personal Access Token

Webex REST API calls require an API access token in the request header. For real-world
applications you want to obtain an access token from a user using a [Webex Integration](https://developer.webex.com/docs/integrations) and OAuth. For testing purposes however you can use your personal access token available in the Developer Portal.

The Webex JS SDK's `init()` takes a JSON object that determines how it will authorize API requests

**To use your personal access token**:

1. Copy your access token from the form below (you must be [signed in](https://developer.webex.com/login) to the Developer Portal).

    

To view or copy your personal access token, open the [official portal page](<https://developer.webex.com/docs/browser-sdk-messaging-tutorial>) and sign in.



2. Open index.js and paste your access token for the value of `access_token`:

    ```javascript
    const webex = (window.webex = window.Webex.init({
        credentials: {
            access_token:
            "<YOUR-ACCESS-TOKEN-HERE>",
        },
    }));
    ```

3. Save your changes to index.js.

## Get a List of Rooms

First you'll use the Browser SDK's [webex.rooms.list()](https://webex.github.io/webex-js-sdk/api/#roomslist) method to get a list of rooms you belong to. The code loops over each [Room](https://webex.github.io/webex-js-sdk/api/#roomobject) object in the results and displays the `title` and `id` property of each object.

1. Add a `listRooms()` function to `index.js` that's called when the user clicks **List rooms**.

    ```javascript
    function listRooms() {
        output.value = "";
        webex.rooms
            .list({ max: 10 })
            .then(function (rooms) {
            if (rooms.items.length == 0) {
                log("There are no rooms to list. Click Create Room.");
            } else {
                for (var i = 0; i < rooms.items.length; i += 1) {
                    log(`${rooms.items[i].title} (${rooms.items[i].id})`);
                }
            }
            }).catch(function (error) {
                log(error);
            });
    }
    ```

2. Open index.html in a browser and click **List rooms**.

    ![App overview](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte8c294887b72ae5a/63485494e72880168de5e4d3/app-overview.png)

## Creating a Room

Next you'll use the [webex.rooms.create()](https://webex.github.io/webex-js-sdk/api/#roomscreate) method to create a new room (space). The `prompt()` method is used to get the room name from the user.

1. Open index.js and add the following code.

    ```javascript
    // Variables to hold new room name and ID
    let newRoomName, newRoomId;

    function createRoom() {
        // Create the room and save room name and ID
        newRoomName = prompt("Enter room name", "My Test Room");
        if (newRoomName) {
        webex.rooms
            .create({ title: newRoomName })
            .then(function (room) {
                output.value = "";
                newRoomId = room.id;
                log(`Created room: ${room.title} with ID ${room.id}`);
            })
            .catch(function (error) {
                output.value += error + "\n";
            });
        }
    }
    ```

2. Save your changes to index.js and reload index.html in your web browser.
3. Click **Create room** and enter a room name at the prompt, then click **OK**.

    ![New room prompt](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte3344838ea1f2cb3/634863fd8e2325105d7c8c07/new-room-prompt.png)

4. Open your Webex app to see the new room you've created.

    ![New room in webex](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf48f8eb458aa4dcb/63486337e72880168de5e861/new-room.png)

## Send a Message to a Room

In this step you'll add code that sends a message to a room using the [webex.messages.create()](https://webex.github.io/webex-js-sdk/api/#messagescreate) method.

**Steps:**

1. Open index.js and add the following `createRoom()` function.

    ```javascript
    let newRoomName;

    function createRoom() {
    // Create the room and set newRoomId to the room's ID
    newRoomName = prompt("Enter room name", "My Test Room");
    if (newRoomName) {
        webex.rooms
        .create({ title: newRoomName })
        .then(function (room) {
            output.value = "";
            newRoomId = room.id;
            log(`Created room: ${room.title} with ID ${room.id}`);
        })
        .catch(function (error) {
            output.value += error + "\n";
        });
    }
    }
    ```

2. Save your changes and load index.html in the browser.
3. Click **Send message**, enter the message text to send at the prompt, then click **OK**.

    Open the Webex app to see the message in the newly created room.

    ![Send message](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltde11c2febbcf8371/634867933b9a3d285e1b6bca/send-message.png)

## Add a User to a Room

Next, you'll use the [webex.memberships.create()](https://webex.github.io/webex-js-sdk/api/#membershipscreate) method to add a user to a room by their email address. You can use any email address, there doesn't need to be Webex account associated it.

**Steps**:

1. Open index.js and create an `addMember()` function, 

    ```javascript
    function addMember() {
        let email = prompt("Enter email of user to add", "user@example.com");
        if (newRoomId) {
            webex.memberships
            .create({
                personEmail: email,
                roomId: newRoomId,
            })
            .then(function (membership) {
                log(`${membership.personEmail} added to room`);
            })
            .catch(function (error) {
                log(error);
            });
        } else {
            log("No room ID. Click Create Room");
        }
    }
    ```

2. Save your changes and open index.html in a browser.
3. Click **Add member to room**, enter an email address at the prompt, then click **OK**.

    Open the Webex app and see that the user has been added to the room.

    ![New user added to space](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltfcc09052cc514094/6348724a0528631ea567e73f/new-user.png)

## Delete a Room

you'll use the [webex.messages.listen()](https://webex.github.io/webex-js-sdk/api/#messageslisten) method to be notified when a message is created or deleted in a room.

1. Open index.js and add the following function:

    ```javascript
    function deleteRoom() {
        let roomId = prompt("Enter ID of room to delete", newRoomId);
        webex.rooms
            .remove(roomId).then(function () {
                output.value = "";
                log("Room deleted");
            }).catch(function (error) {
                log(`Error deleting room ${error}`);
            });
    }
    ```

2. Save your changes and reload index.html in your browser.
3. Click **List rooms** to get a list of rooms.
4. Copy the ID of one of the rooms to your clipboard. It should be a room that you created previously with this app.
5. Click **Delete room by ID**, paste the room ID into the input text field at the prompt, then click **OK**.

Open the Webex app to confirm the room was deleted.

## Listen for New Messages

Next, you'll use the [webex.messages.listen()](https://webex.github.io/webex-js-sdk/api/#messageslisten) method to be notified when a message is created or deleted in a room. 

**Steps**:

1. Open index.js and the following code that defines `startListening()` and `stopListening()` methods that are called when the user presses the corresponding buttons. The app listens for created and deleted message events.

    ```javascript
    function startListening() {
        webex.messages.listen().then(() => {
            // Listen for newly new message events:
            webex.messages.on('created', (event) => log("New message from " + event.data.personEmail + ": " + event.data.text));
            // Listen for deleted message events:
            webex.messages.on('deleted', (event) => log(`Message delete event: ${JSON.stringify(event)}`));
            log("Listening for new messages...")
        }).catch((e) => console.error(`Unable to register for message events: ${e}`));
    }
    
    function stopListening() {
        webex.messages.stopListening();
        webex.messages.off('created');
        webex.messages.off('deleted');
        log("Stopped listening for new messages.")
    }
    ```

2. Save your changes and open index.html in a browser.
3. Click **Start Listening**.
4. Open the Webex app and send a message to any space you belong to, or delete a message. The events are 

    ![Listening for new/deleted messages](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd4276039d09695d7/63488a990528631ea567e787/message-listener.png)
