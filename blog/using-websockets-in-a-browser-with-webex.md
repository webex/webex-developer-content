---
type: Article
title: Using Websockets in a Browser with Webex
canonical_url: https://developer.webex.com/blog/using-websockets-in-a-browser-with-webex
content_type: blog
date: '2020-08-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/using-websockets-in-a-browser-with-webex)

We previously published a blog post on the topic of websockets, where we discussed what exactly websockets are and how you can utilize them in the backend if you run Node.js. We also gave an example showing how to handle incoming message events - triggered by the websocket listener - in a very simple Java app, showcasing some nice cross-language collaboration. If you want to read more about these apps and websockets, check out the blog post [here](https://developer.webex.com/blog/using-websockets-with-the-webex-javascript-sdk).

In this guide, we will walk you through creating and using websockets in a browser-based app, which will listen for events sent from Webex. This would primarily be useful when building an internally focused application, like an intranet site, that needed to exist behind a firewall and not for public use.

### Use case

As mentioned in our previous blog post, websockets can provide a great alternative to webhooks. For example, if you want to listen for events from Webex, like ‘messages:created’, but don’t have a public URL where these events can be forwarded to, you could use websockets to get around the issue. With websockets, you can set up a listener directly in your code that will keep an ear out for incoming events sent by the Webex platform, and you can handle them right in your application. No need for webhooks and public URLs. 

In the following sections, we will go through each step - from creating a websocket listener to getting it running for messages in a browser-based application. In our example, we will build an app with a simple HTML page, which will update every time you receive a message in one of your rooms. This will help validate the websocket is functional during your testing.

### Requirements

Before getting started with websockets, make sure you have everything that is needed to get up and running with the Browser SDK, including Node.js and NPM installed - more information can be found in both the [main documentation page](https://developer.webex.com/docs/sdks/browser) and via the [Github repo](https://github.com/webex/webex-js-sdk/blob/master/README.md). 

In our example, we used Browserify to bundle the SDK and added it in the HTML file with a script tag (Parcel is used in the main docs, either way is fine); the bundle.js file we built is included in the Github repo listed at the end of this guide, if you want to just use ours.

```html
<script src="bundle.js"></script>
```

You will also need an access token with the appropriate scopes – you won’t need it in the application code itself, but will need it later to run the demo, so just grab one and hang on to it for now. For testing purposes, you can use the Developer token accessible in a few places in the developer portal documentation (like the [Getting Started](https://developer.webex.com/docs/api/getting-started) page) but note that the token will expire in a very short window of time (currently 12 hours) so for anything production you will want to use a bot or integration token (depending on what data you’re trying to retrieve).

### Creating a Websocket listener


#### Step 1: Authentication

This is the place where we will use the previously requested access token. It will be entered into a field in the HTML web page when the demo is launched and is needed for the demo to function. Following good practices, we do not extract and then hardcode the access token in our code, rather we read the value of our Access Token field from the HTML file:

```javascript
webex = Webex.init({
    credentials: {
        access_token: document.getElementById('access-token').value
    }
});
```

Please note, initializing Webex this way does not verify if your access token is valid or not. While it won’t be difficult to verify your own token (you went and grabbed it from the developer portal yourself), in a production app used by others, you would want to handle that case by making a validating request. A good option is to make a GET call to /people/me and handle the returned Promise:

```javascript
//makes a call to /people/me to verify that the passed access-token is valid
//if it is, shows further options, like 'Listen to messages',... are activated
webex.people.get('me').then(person => {

    //access token is verified

    tokenHolder = person;

    document.getElementById('authenticate-message').innerHTML = 'authenticated as '
        + tokenHolder.displayName;
    document.getElementById('authenticate-message').classList.remove('label-warning',
        'label-error');
    document.getElementById('authenticate-message').classList.add('label-success');

    //show further options
    document.getElementById('option-wrapper').style.display = 'inline';
    document.getElementById('message-wrapper').style.display = 'inline';

    document.getElementById('authenticate-button').disabled = true;

}).catch(reason => {

    //access token expired

    document.getElementById('authenticate-message').innerHTML = 'authentication failed';
    document.getElementById('authenticate-message').classList.add('label', 'label-error');

});
```

#### Step 2: Start listening

Since we only want to listen for messages, our app uses the listen() function of this resource only. Once the listener is started, you can call the on() function to specify which event you want to listen for. The most basic version of this command looks like this:

```javascript
webex.messages.listen()
    .then(() => {
    console.log('listening to message events');
    webex.messages.on('created', (event) => {console.log(`Got a message:created event:\n${event}`);
     })
     .catch((e) => {console.error(`Unable to register for message events: ${e}`));
```

Our example is extended with updating the UI with the data extracted from the received ‘messages:created’ event. We also make two GET calls to receive more detailed information about the message and show on the UI who posted it and in which room. With the response of the GET calls, we can display person names and room titles and not just the respective ID.

```javascript
//creating the websocket listener with 'messages' resource...
webex.messages.listen().then(() => {

    //updating UI
    document.getElementById('listen-message').innerHTML = 'listening to messages';
    document.getElementById('listen-message').classList.remove('label-warning');
    document.getElementById('listen-message').classList.add('label-success');
    document.getElementById('listener-btn').innerHTML = 'Stop Listening to Messages';

    //setting global variable to keep track of the listener
    listening = true;

    //...and 'created' event
    webex.messages.on('created', (event) => {

        //message is received in any of the token holders rooms
        console.log('message received');

        //logging the time of the event and putting it into a user friendly format
        const date = new Date(Date.parse(event.data.created));
        const dateToDisplay = date.toTimeString().split(' ')[0];

        //getting the details of the message sender to update the UI
        webex.people.get(event.actorId).then(
            sender => {

                //getting the details of the room the message was posted in
                webex.rooms.get(event.data.roomId).then(
                    room => {

                        //update UI
                        document.getElementById('message-room-title').innerHTML = room.title;
                        document.getElementById('message-posted').innerHTML = event.data.text;
                        document.getElementById('message-sent-by').innerHTML = sender.displayName;
                        document.getElementById('message-sent-at').innerHTML = dateToDisplay;
                    }
                ).catch(reason => {

                    //could not get room details for some reason
                    console.error(reason.message);
                });
            }
        ).catch(reason => {

            //could not fetch person details
            console.error(reason.message);

        });

    })

}).catch(error => {

    //listener / websocket could not be started
    console.error(error.message);

});
```

#### Step 3: Stop listening

Cleaning up the listener will also be done from your app code by calling the stopListening() and the off() functions provided by the SDK. Please note, that both of these commands are required to stop the websocket listener.

```javascript
webex.messages.stopListening();
webex.messages.off('created');
```

### The HTML file

The html file we used in this example is quite straight-forward, separated into a few distinct parts that divide the page into logical units. We start with the text description, standard heading and paragraph separations:

```html
<div class="container">
    <div class="columns">
        <div class="column col-12">
            <h2>Websocket Listener</h2>
            <h3>Start listening to Webex messages in the browser </h3>
            <p>After a successful authentication further options will appear on the screen, such as:
                <br><b>Start Listening to Messages -</b> activates the websocket listener and sends
                a notification when a message is posted into one of your rooms.
                <br>
                <b>Create Test Room -</b> you can create your own test room,
                where you can post random messages to speed things up.
            </p>
            <p>You can find the source code for this application <a href="app.js" target="_blank">here</a></p>
            <hr>
```			

Then, we setup the authentication form. This is where the user of the demo will enter in their token on the web page (which we extract in the app code described earlier):

```html
<form class="form-group" id="authenticate">
    <fieldset>
        <label class="form-label" for="access-token">Your Personal Access Token
            <br>
            <a href="https://developer.webex.com/docs/api/getting-started" target="_blank">Request one
                here</a>
            <br></label>
        <input
                class="column col-8"
                id="access-token"
                name="accessToken"
                placeholder="Personal Access Token"
                type="text"/>
        <button class="btn" id="authenticate-button" type="submit" title="submit">Authenticate</button>
    </fieldset>
    <div class="label: label label-rounded" id="authenticate-message">not authenticated</div>
    <br/>
    <div class="label: label label-rounded" id="listen-message">not listening to messages</div>
</form>
```

And then, we have a few wrappers:

The Options Wrapper (initially hidden) groups the additional buttons, like Start Listening to Messages:

```html
<div id="option-wrapper" ... </div>
```

The Room Wrapper (initially hidden) contains a table for displaying the test room details:

```html
<div id="room-wrapper" ... </div>
```

The Message Wrapper (initially hidden) contains a table for displaying the messages the user receives after activating the listener:

```html
<div id="message-wrapper" ... </div>

        </div>
    </div>
</div>
```

The full code for our demo application, including the bundle.js file, app.js file and the index.html file, can be found [here](https://github.com/webex/websocket-demo-page).  Once you have all of the files in the same directory, simply open the index.html file in your browser to run the application. 

If you have any questions, please don’t hesitate to contact support via devsupport@webex.com.
