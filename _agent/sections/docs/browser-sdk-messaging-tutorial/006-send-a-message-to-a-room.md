---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Send a Message to a Room
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
