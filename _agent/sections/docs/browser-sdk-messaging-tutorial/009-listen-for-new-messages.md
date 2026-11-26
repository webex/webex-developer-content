---
type: Excerpt
canonical_url: https://developer.webex.com/docs/browser-sdk-messaging-tutorial
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Listen for New Messages
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/browser-sdk-messaging-tutorial). [Full Markdown](../../../../docs/browser-sdk-messaging-tutorial.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

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
