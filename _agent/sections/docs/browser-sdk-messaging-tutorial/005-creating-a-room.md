---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating a Room
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
