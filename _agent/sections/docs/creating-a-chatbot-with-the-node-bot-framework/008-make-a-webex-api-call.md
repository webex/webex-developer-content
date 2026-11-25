---
type: Excerpt
canonical_url: https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Make a Webex API Call
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/creating-a-chatbot-with-the-node-bot-framework). [Full Markdown](../../../../docs/creating-a-chatbot-with-the-node-bot-framework.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Prerequisites](002-prerequisites.md)

## Article introduction

Learn how to create a chat bot using the Node Bot Framework.

## Selected section

## Make a Webex API Call

Each bot instance provides a reference to a Webex JavaScript SDK instance that your app can use to make calls against that SDK. For instance, you could use [memberships.list()](https://webex.github.io/webex-js-sdk/api/#membershipslist) to get a list of members in a space so you can send each a direct message using the [bot.dm()](https://github.com/WebexSamples/webex-node-bot-framework/blob/master/README.md#Bot+dm) method, as shown below.

**To send a DM to each user in a space**:

1. Open index.js in the starter bot project.
2. Add the following code that listens for a `poke` command.

    ```javascript
    framework.hears("poke", function (bot, trigger) {
      responded = true;
      // Use the webex SDK to get the list of users in this space
      bot.webex.memberships.list({roomId: bot.room.id})
        .then((memberships) => {
          for (const member of memberships.items) {
            if (member.personId === bot.person.id) {
              // Skip myself!
              continue;
            }
            // Get name of poker
            let pokerName = (member.personDisplayName) ? member.personDisplayName : member.personEmail;
            bot.dm(member.personId, `You got poked by ${pokerName}`);
          }
        })
        .catch((e) => {
          console.error(`Call to sdk.memberships.get() failed: ${e.messages}`);
        });
    });
    ```
  
3. Save your changes and restart the Node server (`npm start`).

Once the server indicates it's listening for Webex events, send a "poke" message to the space and tag the bot by name. The bot will send a DM to each member in the space.
