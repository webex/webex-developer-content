---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Delete a Room
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
