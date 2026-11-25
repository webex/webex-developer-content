---
type: Excerpt
canonical_url: https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- Experience the Space Widget
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/using-the-webex-space-widget-for-video-and-messaging). [Full Markdown](../../../../docs/using-the-webex-space-widget-for-video-and-messaging.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Selected section

## Experience the Space Widget

The Space widget handles coordination between your application and the Webex APIs: it provides fully functional, ready-to-use components of the Webex meeting user interface ready to drop into you existing web page.

The Space widget (as of this writing) supports the following features:

* 1-on-1 and group space messaging
* 1-on-1 and group space video calling
* Space roster list and @mentions
* Dialing by email address or SIP address
* Inline Markdown formatting
* Sharing of files and documents
* Previewing and downloading of files and documents
* Flagging messages for follow-up



> **Info**
>
> Whiteboard features are not supported by the current version of the Widget.  See the [Widget GitHub repo](https://github.com/webex/react-widgets/tree/master/packages/node_modules/@webex/widget-space) for the latest details on feature/browser support.



The demo requires two inputs:

* A Webex API access token.
* The ID of a Webex meeting, or the email address of a Webex user, with whom to start a collaboration session

**To experience the Space widget:**

1. Sign in to the [Developer portal](https://developer.webex.com).
1. Go to the [Accounts and Authorization](https://developer.webex.com/docs/getting-started#accounts-and-authentication) section of the [Getting Started](https://developer.webex.com/docs/api/getting-started) page. 

1. Click the copy icon at the right of the "Bearer ****" text field to copy your personal access token to your clipboard.

    ![Personal access token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2b104c66a752a7dc/61e8807eb7138d58986f5636/webex4devs-access-token.png)

1. Using Firefox, Google Chrome or Safari, navigate to the [Space widget demo page](https://code.s4d.io/widget-demo/production/index.html).

1. In **Webex Access Token** panel, select **Access Token**, and paste your access token into the **Token** field:

    ![Pasting access token](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltb134c10538a4c6f6/demo-form-token.png)

1. Click **Save Token**.

1. In the **Space Widget** panel, make the following selections:

    * Set **Widget Destination Type** to **To Person**.
    * Set **Widget Initial Activity** to either **Message** or **Meet**.
    * Under **Widget Activities** select all activities.
    * Under **Widget Composer Actions** select **Attach Files**.

    ![Selecting widget options](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte23805f2c20a157e/demo-form-select-options.png)

1. In the **Widget Destination** field, enter in the email address of the Webex user you wish to start the collaboration session with.  

    ![Email of user with whom to collaborate](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltddc7522e14c1ce87/61e8807ea1a3da10d297ccc9/demo-form-choose-id.png)
    
    Notes:
    * If you don't have another Webex user to call, you can enter `loopback@rtp.ciscotac.net`, or create a second Webex account using an alternate email address. This will let you send messages to the loopback user, but you won't be able to make a video call, for which you need to specify a real Webex user.
    * Don't use the same Webex account to both obtain the access token and use as the Widget destination as you can't call yourself!

    Now you’re ready to test!

1. Click **Open Space Widget** to experience the Space widget live in 1-on-1 mode. 

    

> **Info**
>
> If you don't see the widget, scroll down on the page. Click "Stick Widgets" to have the widget appear at the top of the page.



1. Post a few messages, drag-and-drop a file into the Space, and confirm that these activities are reflected in the destination user's Webex client.

1. Click the green call button in the upper-right corner initiate an video call.

    You’ll be asked for the authorization to access your camera and microphone.

    

> **Info**
>
> Note that you did not need to install any additional software to have the video call, as the Space widget takes advantage of standards-based [HTML5 WebRTC](https://webrtc.org/) functionality built into the browser to handle all audio/video functions.
