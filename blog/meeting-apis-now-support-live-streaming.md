---
type: Article
title: Meeting APIs Now Support Live Streaming
canonical_url: https://developer.webex.com/blog/meeting-apis-now-support-live-streaming
content_type: blog
date: '2025-03-27'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/meeting-apis-now-support-live-streaming)

There was a great update recently released for the Meeting APIs that enables hosts to setup [live streaming of their meetings and webinars](https://help.webex.com/en-us/article/a6cmw/Live-stream-meetings-and-webinars) through various services, such as [IBM Video Streaming](https://help.webex.com/en-us/1gt29d/), [Facebook Live](https://help.webex.com/en-us/ka80pdb/), [Vbrik Rev](https://help.webex.com/en-us/i7a7v6/), and [YouTube Live](https://help.webex.com/en-us/d9zqvi/). This feature is ideal to help your meetings reach a wider audience for product launches, company announcements, expert panel discussions and more. Another benefit of this feature is that instead of having to make an exhaustive list of meeting invitees, you can simply provide a link to your live stream, and anyone can view your live stream quickly and easily. Now that this can be enabled via the Meetings APIs, you can completely automate the process to set up a live stream of any Webex meeting or webinar and optimize efficiency.

### Live Stream Attributes in the Meeting APIs

Some new attributes have been added in the [Create a Meeting](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting), [Patch a Meeting](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting), and [Update a Meeting](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting) endpoints to set up live streaming. The main attribute that needs to be set first is `enabledLiveStream`, that can be `true` or `false`.  When `enabledLiveStream` is set to `true`, an object called `liveStream` is then required to configure the live stream settings of the meeting using the following parameters:

- `destination`*(required)* - this is a text string that describes the destination of the live stream, such as “YouTube”.
- `rtmpURL`*(required)* – this is for the *ingestion* stream that is used for sending the live video content from the Webex meeting to a streaming service. Refer to your specific live streaming service for this information.

    The URL will use the `rtmp/s` protocol such as: `rtmps://example.com:1935/LiveMedia/WebexMeetingStream`.

- `streamURL`*(required)* – this is for the *playback* URL to view the Webex meeting live stream. This URL should use the M3U8 video format for HTTP Live Steaming (HLS), which is supported across a wide range of devices, including iOS &amp; Android devices, modern web browsers, smart TVs, and streaming devices. Again, refer to your live streaming service to obtain this information.
    The `URL` may look something like this example: `https://example.com/WebexStreaming/index_a.m3u8`
- `layoutWithoutSharedContent` – this parameter sets the meeting layout that will be displayed on the live stream when no content is being shared. Any one of these strings are accepted:
  - `grid` – layout to see multiple meeting participants in a grid
  - `stack` – layout to display the active speaker on the stage and up to six participants in thumbnails across the top
  - `focus` - layout that only displays the active speaker
- `layoutWithSharedContent` – sets the meeting layout that will be displayed on the live stream when there is content being shared. The following strings are accepted in this field:
  - `stack` – layout to display the shared content on the stage and up to six participants in thumbnails across the top
  - `focusedContentWithActiveSpeaker` – layout to display the shared content in the main part of the screen and a large thumbnail of the active speaker in the upper right corner
  - `focusedContent` – layout that only displays the shared content in the main part of the screen and does not display the participants
- `allowChangeLayoutInMeeting` – when set to `true`, it will allow the changing of the live streaming layout in the meeting.
- `followStageLayoutWhenSynced` – when set to `true`, it will follow the stage layout when being [synchronized](https://help.webex.com/en-us/article/nic6kmbb/Sync-your-stage-with-everyone-in-meetings,-webinars,-and-events>).
- `resolution` – this string sets the resolution of the live steam, such as `1920x1080`. If not specified, the default setting is `720x1280`.

In summary, the live stream setup in a [Create](https://developer.webex.com/docs/api/v1/meetings/create-a-meeting)/[Patch](https://developer.webex.com/docs/api/v1/meetings/patch-a-meeting)/[Update](https://developer.webex.com/docs/api/v1/meetings/update-a-meeting) Meetings API request will include something like this in the JSON body:

```json
{
    "enabledLiveStream": true,
    "liveStream": {
        "destination": "YouTube",
        "rtmpUrl": "rtmps://example.com:1935/LiveMedia/WebexMeetingStream",
        "streamUrl": "https://example.com/WebexStreaming/index_a.m3u8",
        "layoutWithoutSharedContent": "grid",
        "layoutWithSharedContent": "stack",
        "allowChangeLayoutInMeeting": false,
        "followStageLayoutWhenSynced": true,
        "resolution": "1920x1080"
    }
}
```

### Enabling the Webex Meeting Live Streaming Feature for Testing

The Live Stream feature for Webex Meetings is not turned on by default and must first be enabled by a Webex administrator in Control Hub to start testing it. The best route to start testing the API is by using a free [Developer Sandbox](https://developer.webex.com/docs/developer-sandbox-guide), which provides admin access to a Webex org of your own. Once you log into Control Hub as an admin, you will need to enable live streaming services on your Webex site, enable live streaming for individual users, and enable the live stream video resolutions. Refer to [this help article](https://help.webex.com/en-us/article/xk37so/Enable-live-streaming-in-Webex-Meetings-and-Webex-Events) for the most up-to-date information on applying these settings inside of Control Hub.

After you enabled the proper settings in Control Hub and setup the live stream with the Meetings API, you are ready to test it. First, start the meeting in the Webex app as the host. When the meeting is active, start live streaming from the meeting client by selecting the *three dots*, click **Start live streaming** and then **Go live**. You can then head over to your live streaming service to watch your meeting broadcast as a regular viewer.

### Need Some Help? No Problem

As always, we are standing by to provide developer support for any of the API features in this article. If you need help or have any questions, the [Webex Developer Support Team](https://developer.webex.com/support) is eager to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity). Until next time, happy developing!
