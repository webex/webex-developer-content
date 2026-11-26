---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Add a User to a Room
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
