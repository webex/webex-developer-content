---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Get a List of Rooms
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
