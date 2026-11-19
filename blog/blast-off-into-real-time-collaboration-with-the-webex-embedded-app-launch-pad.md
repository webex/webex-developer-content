---
type: Article
title: Blast Off into Real-Time Collaboration with the Webex Embedded App Launch Pad
canonical_url: https://developer.webex.com/blog/blast-off-into-real-time-collaboration-with-the-webex-embedded-app-launch-pad
content_type: blog
date: '2025-03-11'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/blast-off-into-real-time-collaboration-with-the-webex-embedded-app-launch-pad)

I'm a huge fan of [Jackbox](https://www.jackboxgames.com/) games, and one of the things I love about their lobby system is how it allows users to customize their avatar and display name before the game starts. This feature makes the experience much more immersive and engaging.

[Webex Embedded Apps](https://developer.webex.com/docs/embedded-apps) provide developers with the power to integrate seamless, real-time experiences directly within Webex Meetings. To accelerate development, we are excited to introduce the [Webex Embedded App Launch Pad](https://github.com/WebexSamples/ea-lobby-app): a prebuilt solution that allows developers to quickly add a multi-user collaboration lobby to their web applications for use in Webex Meetings with the [Embedded App SDK](https://eaf-sdk.webex.com/) already integrated.

With this launchpad system, you can enable users to gather in a shared virtual space before launching an interactive embedded app experience. Whether for team planning, brainstorming, or gaming, this tool enhances real-time collaboration inside of a Webex Meeting.

### Why a Lobby System in Launchpad?

A collaboration lobby is a well-established concept in real-time gaming and collaboration applications. It provides participants with a place to join, prepare, and configure settings before starting a shared activity. In the context of Webex Embedded Apps within a Webex Meeting, a lobby can be leveraged for:

- **Planning poker sessions**: Allow teams to prepare before launching a sprint planning tool.
- **Online multiplayer games**: Give participants a space to join teams and roles before starting the game.
- **Real-time surveys or polls**: Let users join and confirm participation before pushing a live interactive poll.

<br/>

### Key Features

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb01912b607c0eabf/embedded-app-launchpad-starter-app-2.png)

The Webex Embedded App Launch Pad provides the following out-of-the-box capabilities:

- **Lobby Creation**: Hosts can create a new lobby with a unique identifier.
- **Participant Management**: Users can join a lobby and update their display name.
- **Ready-Up Status**: Participants can mark themselves as "ready," signaling they are prepared to start.
- **Real-Time Updates**: Lobby participants and status changes are synchronized across all users via WebSockets.
- **Seamless Webex Integration**: Automatically fetch Webex user details and meeting context.
- **Webex Embedded Apps Ready**: Built in support for launching your app to all Webex Meeting participants.

<br/>

### How It Works

Here are details on how the launchpad’s lobby works:

1. Create a Lobby
    A Webex user launches the Embedded App and creates a new lobby. The app automatically pulls in the Webex meeting title and sets it as the default lobby name from the [Meeting State SDK object](https://eaf-sdk.webex.com/interfaces/IWebexAppsMeetingState.html). The creator of the lobby will also have their name pre-populated via the [User State SDK object](https://eaf-sdk.webex.com/interfaces/IWebexAppsUserState.html).
1. App Opened for all Participants
    The lobby host then tells Webex to open the lobby URL via the [SetShareURL method](https://eaf-sdk.webex.com/classes/Application.html#setShareUrl) in the SDK. This will open the lobby for everyone in the Webex Meeting.
1. Participants Join
    Other meeting attendees can join the lobby directly from their Webex meeting session. Each participant is assigned a unique identifier and can update their display name, which is defaulted to their Webex display name.
1. Interact in the Lobby
    - Users can see who has joined and their "ready" status.
    - The host can monitor the participants and control when to start the activity.
    - The WebSocket-based backend ensures instant updates for all users.
1. Transition to the Main Experience
    Once all users are "ready," the lobby can transition into the main embedded app experience: whether a game, a planning session, or a collaborative tool.

<br/>

### Getting Started

Detailed instructions are provided in the in [repository’s README file](https://github.com/WebexSamples/ea-lobby-app), but we will hit the highlights here. Before continuing, make sure you’ve got Node.js version 20 or above, Python3, as well as Git installed.

#### Installation

Clone the repository and set up the backend and frontend services:

```bash
git clone https://github.com/WebexSamples/ea-lobby-app.git
cd ea-lobby-app
```

#### Backend Setup

Configure the backend:

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows, use 'venv\Scripts\activate'
pip install -r requirements.txt
python -m backend.app
```

#### Frontend Setup

Configure the frontend:

```bash
cd frontend
npm install
npm run dev
```

### Code Highlights: ‘useWebex’ Hook

Since our Launchpad is a React application, we’ve decided to encapsulate all of the Webex SDK functionality into a single “[useWebex](https://github.com/WebexSamples/ea-lobby-app/blob/main/frontend/src/hooks/useWebex.jsx)” [React Hook](https://react.dev/reference/react/hooks). This allows us to quickly get to information about the Webex User, the Webex Meeting, and even the Webex SDK itself in one shared location! For example, you’ll see that our [main application file](https://github.com/WebexSamples/ea-lobby-app/blob/main/frontend/src/App.jsx) accesses the theme from the SDK via the hook. We also use the meeting and user name to prepopulate the lobby in the [lobby creation component](https://github.com/WebexSamples/ea-lobby-app/blob/main/frontend/src/components/CreateLobby.jsx). While the “useWebex” hook doesn’t encapsulate ALL functionality from the SDK, it certainly makes things much easier! That being said, pull requests for expanding the hook are always welcomed.

### Testing in Webex

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltaf7f637ba5eaca4e/embedded-app-launchpad-starter-app-3.png)

Since Webex Embedded Apps are meant to be run inside a Webex context, testing the app during development can be a tedious process. You have to deploy the app somewhere, start a meeting, launch the app from within the meeting, and then finally you can test out your feature development. Luckily, Webex engineers have provided us with an easy solution, the [Embedded Apps Meeting Emulator](https://eaf-sdk.webex.com/samples/thinclient.html)! This tool will allow you to iframe in any application, including localhost, and provide the Embedded App SDK with mock data and events. You can even open up web inspector and debug your app!

### Deploying in Webex

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7d0840bafe44c686/embedded-app-launchpad-starter-app-4.png)

To embed this app in a Webex meeting:

1. Register an Embedded App in the [Webex Developer Portal](https://developer.webex.com/).
1. Setup the app to run in the Webex Meeting context.
1. Configure the app to include the proper domains.
    

> **Info**
>
> Embedded apps require a publicly accessible HTTPS address.


1. Deploy your backend and frontend to a publicly accessible server.

<br/>

### Conclusion

Now that your app has successfully lifted off with the Webex Embedded App Launch Pad, you can focus on crafting an out-of-this-world experience for your users. No need to worry about setting up Webex connections or ensuring participants are ready—this launch pad has you covered, so you can concentrate on building an app that truly reaches for the stars!

The [Webex Embedded App Launch Pad](https://github.com/WebexSamples/ea-lobby-app) simplifies the process of adding real-time collaboration features to your Webex apps. Whether you’re building a game, a voting system, or a brainstorming tool, this project provides a plug-and-play solution for managing participants before launching an interactive session.

Try it out today and take your Webex Embedded Apps to the next level!
