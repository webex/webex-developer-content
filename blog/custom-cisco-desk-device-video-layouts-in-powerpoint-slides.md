---
type: Article
title: Custom Cisco Desk Device Video Layouts in PowerPoint Slides
canonical_url: https://developer.webex.com/blog/custom-cisco-desk-device-video-layouts-in-powerpoint-slides
content_type: blog
date: '2023-11-06'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/custom-cisco-desk-device-video-layouts-in-powerpoint-slides)

The devices in the [Cisco Desk series](https://www.cisco.com/c/en/us/products/collaboration-endpoints/webex-desk-series/index.html) for [RoomOS](https://www.cisco.com/c/en/us/products/collaboration-endpoints/collaboration-room-endpoints/roomos.html) have some great capabilities for sharing live content in meetings and calls. One of the amazing ways Desk devices can enable more captivating presentations is with the [Immersive Sharing](https://help.webex.com/en-us/article/nmhu88ab/Immersive-share-on-Desk-Series) feature. This feature allows the audience to keep focus on both the presenter and the content, by adding an overlay of the camera video within the presentation channel. With Immersive Share, you can use the touchscreen on the Desk device to change the position and size of your camera video embedded within the presentation content, both before and during the share. 

However, what if you want to present PowerPoint slides that require custom layouts for each slide, so the Desk device camera video is properly sized and in the right location based on the content? To see how this can be this can be done through the power of [macros](https://help.webex.com/en-us/article/gj962f/Configure-macros-and-user-interface-extensions-for-Board,-Desk,-and-Room-Series) and the [roomOS xAPI](https://roomos.cisco.com/xapi), you can leverage a great demo: *the Webex Desk Slide Presenter integration*.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt65588c4b02e05582/cisco-desk-series-video-in-powerpoint-slides-2.png)

### About the demo

The demo was created by Joe Hughes and arranged by Dirk-Jan Uittenbogaard, both Cisco Technical Solutions Architects. The original instructions can be found on the [Cisco Community Forums](https://community.cisco.com/t5/collaboration-blogs/deskpro-video-in-powerpoint-slides/ba-p/4702630) and now updated here for this blog. To get started, just follow the steps below to run the demo and see it in action. The macro enabled PowerPoint slides that are included also make great templates to repurpose for your own immersive presentations.

### Brief explanation

With this integration, eachPowerPoint slide controls **where/how big **your camera video appears on the screen by looking for a specially named shape. The complete demo can be found on [GitHub](https://github.com/vtjoeh/webex-desk-slide-presenter) and the components are as follows:

1. xAPI macro: [WebexDeskSlidePresenter.js](https://github.com/vtjoeh/webex-desk-slide-presenter/blob/main/WebexDeskSlidePresenter.js)
    This JavaScript file will be deployed to the Desk device as an [onboard macro](https://roomos.cisco.com/doc/TechDocs/Integrations#macros) that enables custom control of the Immersive Share feature. For more information on how to work with the xAPI, check out the [tech docs](https://roomos.cisco.com/doc/TechDocs/xAPI). 
1. PowerPoint file that contains a macro: [TemplateDeskProMacro_verXX.pptm](https://github.com/vtjoeh/webex-desk-slide-presenter/blob/main/TemplateDeskMacro_ver0.1.5.5.pptm)
1. Users can also create macros inside a PowerPoint presentation. The PowerPoint macro created for the slides in this demo does the following:
    - Checks if the slide contains a shape with a special name to indicate where the video should be placed
    - Calculates where the Desk device should put (your) camera feed and how big it should be
    - Sends API calls to the Desk device to put your video in the right location.
    - PowerPoint file that contains a macro (`TemplateDeskProMacro_verXX.pptm`)

<br/>

### Requirements

In order to run this demo integration, you will need the following:
- Webex video device: Desk, DeskMini, DeskPro
- Video device: ability to add a user (administration)
- Macro-enabled PowerPoint slides (included)
- The computer running PowerPoint to be on the same network as the Webex Desk device 

<br/>

### How to setup the demo

For a quick rundown on how to use this demo, check [out this great Vidcast](https://app.vidcast.io/share/1ca0edeb-4bb6-4e7e-af7a-b49f74530183) by Dirk-Jan Uittenbogaard. 

Before you start, download [this ZIP](https://github.com/vtjoeh/webex-desk-slide-presenter/archive/refs/heads/main.zip) file from [GitHub](https://github.com/vtjoeh/webex-desk-slide-presenter). It contains the 2 files you need: the `.PPTM` file and the `.JS` file.

1. **Desk device:** Use the web IP to access the device and log in. For administrator setup, see [this help article](https://help.webex.com/en-us/article/n5pqqcm/Device-configurations-for-Board,-Desk,-and-Room-Series-devices) for more information.
1. **Desk device:** Under SETUP, click **Users** and then "Create User".
    **Role:** only 'RoomControl'
    **Password:** you decide
1. **Desk device**: Under CUSTOMIZATION click *Macro editor*, then "Import from file".
    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1f97fd20cfae0a28/cisco-desk-series-video-in-powerpoint-slides-3.png)
1. **PowerPoint:** Open the downloaded PPTM (M=Macro) file
  1. When the popup is shown, click "enable macros"
  1. On slide 1, enter the IP-address of your (locally accessible) Desk Pro + the username/password you created in the previous step. Note that when you go into presentation view and click the "start macro" button, your password will be hidden.
        ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltbbb8757b9e6a126e/cisco-desk-series-video-in-powerpoint-slides-4.png)
1. PowerPoint: Start your presentation
  1. Start slideshow on slide 1 and click "Start Macro" (and confirm that you want to run the macro)
  1. The password is now invisible, and the presentation can start. Click the 'self-view toggle' button to check if you appear in the test box below the start button.



> **Info**
>
> In step 5, item 2 you RUN the PowerPoint macro. You will have to run the macro *every time* you open this PowerPoint presentation.



### Make your own macro-enabled slides

Now that you have the demo running and can see how the integration works, you should be ready to design and present your own immersive slides using the PPTM deck as your template. Here are the steps to get started:

1. Open the `.PPTM` file.
1. RUN the Macro (Remember: you always must do this when opening this `.PPTM` file).
1. Copy slides from your original presentation.
1. Paste your slides in the .`PPTM` file (and "keep formatting"). Paste them AFTER SLIDE 1 because that is needed for the integration with the Desk device.
1. On every slide where video needs to be added, add a 'rectangle' shape (best to keep a 16:9 ratio).
  1. Right-click on the shape.
  1. Select "Size and Position”.
  1. Set *Height* to **4.5** and *Width* to **8** (16:9 aspect ratio).
  1. Click on "Lock aspect ratio”.
  1. Now you can resize and position the square.
1. Select the **rectangle** and open the "selection pane" to "rename" the rectangle

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9592f2fa69e93605/cisco-desk-series-video-in-powerpoint-slides-5.png)

1. RENAME your rectangle to "VideoSquare" or any of the names listed below under "Video embed options" below. The shape name defines its appearance.
1. Go into presentation mode and see your video appear in the slide (don't forget to look at the Desk device [self-view](https://help.webex.com/en-us/article/6895sz/Access-and-adjust-selfview-on-Board,-Desk,-and-Room-Series)).

### Video embed options

This demo has a variety of options for creating immersive slides, providing a lot of flexibility. The descriptions for each of the video layouts contained in the demo slides are referenced in the matrix below.

<table>
    <tr>
      <td></td>
      <td><strong>NAME</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td><strong>IN-CALL ONLY?</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td><strong>Video Channel</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td><strong>Video on Slide</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td><strong>Background</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td><strong>Notes</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>VideoSquare</strong></td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>transparent</td>
      <td>Or use 'VideoShape'</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>VideoSquare_50</strong></td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>transparent</td>
      <td>(1-100) Transparency number</td>
    </tr>
    <tr>
      <td colspan="2"><strong>VideoSquare_PiP</strong></td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>real</td>
      <td>Pip with your physical background</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>VideoSquare_FlipPip</strong></td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>real</td>
      <td>Reverse Pip (PPT small, you big)</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>CameraOnly</strong></td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>current</td>
      <td>Show camera, no slide</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>ContentOnly</strong></td>
      <td>-</td>
      <td>no</td>
      <td>no</td>
      <td>-</td>
      <td>Slide without video</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>SideBySide_[123x]</strong></td>
      <td>✓</td>
      <td>no</td>
      <td>yes</td>
      <td>current</td>
      <td>Slide and video same size</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>SideBySide_[123x]_u</strong></td>
      <td>✓</td>
      <td>yes</td>
      <td>no</td>
      <td>current</td>
      <td>1=Cam, 2=PC(USBc), 3=HDMI, u=mute video</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>Prominent</strong></td>
      <td>✓</td>
      <td>no</td>
      <td>yes</td>
      <td>current</td>
      <td>Small video outside big content</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>StopContentShare</strong></td>
      <td>✓</td>
      <td>no</td>
      <td>yes</td>
      <td>current</td>
      <td>Stops sharing PPT</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>StopImmersiveShare</strong>&nbsp;&nbsp;</td>
      <td>✓</td>
      <td>yes</td>
      <td>no</td>
      <td>current</td>
      <td>Keeps sharing, video moves to video channel</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>SpeakerTrackDiagnostic</strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td>-</td>
      <td>no</td>
      <td>yes</td>
      <td>real</td>
      <td>Send Speaker track in content channel</td>
    </tr>
    <tr>
      <td></td>
      <td><strong>PreviousSlide</strong></td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>Uses the previous slide's command</td>
    </tr>
</table>

There are some other important guidelines to note:

- You can only have 1 object per slide.
- The names are *not* case-sensitive.
- The VideoSquare object can be transparent (i.e. invisible).

<br/>

### Demo FAQs

**Q: Where does the video go?**

*A: This mechanism uses immersive share. That means the PowerPoint with your video is shared in the content channel and people can also see you via video (thumbnail)*

**Q: What if I have a virtual background configured?**

*A: That won't be visible except with the "CameraOnly" object.*

**Q: What if a slide does not have any of these boxes?**

*A: Immersive share will stay engaged (no camera) and the slide (PC source) will still be visible.*

**Q: Can I use shapes like circles, triangles, etc.?**

*A: You could but it doesn't help you because the DeskPros video shape is a square, 16:9*

**Q: How can I quickly create a 16:9 shape?**

*A: Create a square, double click it, under size uncheck "lock aspect ratio", make the height:9 width:16, check "aspect ratio", now resize*

**Q: I don't see my video!**

*A: Did you configure and double-check everything as described above? Did you start the macro?*

**Q: I see my video but not on a specific slide?**

*A: Does the rectangle that you created have the right name?*

*A: Did you group the rectangle? (you should not)*

### Need some help? We Got You Covered!

As always, support is available if you have any questions or need some guidance. For help with Cisco RoomOS xAPI and device macros, check out their [dedicated support channels](https://roomos.cisco.com/support). If you need assistance with the other APIs covered here on the [Developer portal](https://developer.webex.com/), the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to help.
