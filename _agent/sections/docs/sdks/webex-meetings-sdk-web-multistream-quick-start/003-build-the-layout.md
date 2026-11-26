---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Build the Layout
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-multistream-quick-start). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-multistream-quick-start.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Setup Remote Media Event Listeners](004-setup-remote-media-event-listeners.md)

## Article introduction

With multistream, developers gain greater flexibility when displaying remote media streams. Instead of receiving a single stream featuring all participants, multistream enables the showcasing of multiple streams simultaneously. This means you can easily view each remote participant's stream individually, enhancing clarity and engagement during collaborative sessions.

---

This guide provides a quick glimpse into consuming multistream in Webex Meetings using the Webex JavaScript SDK. You'll find code snippets below that can quickly get you up and running.

## Selected section

## Build the Layout

The layout determines how the various streams are positioned and displayed in the user interface. In order to create the layout with remote streams:

1. Create HTML container elements (for example a `<div>`) for the video streams:

    ```html
    <div id="multistream-remote-video" style="display: flex">
      <!-- All the remote videos will render here -->
    </div>
    ```

1. For each streams
    1. Create an HTML `<video>` element and attach the `remoteMedia.stream`.

        ```js
        // Create an html "video" element and attach the `remoteMedia.stream`
        function createVideoElement(stream) {
          const videoElement = document.createElement('video');
          videoElement.srcObject = stream;
          videoElement.height = 480;
          videoElement.width = 620;
          videoElement.autoplay = true;
          videoElement.muted = true;

          return videoElement;
        }
        ```

    1. **(Optional)** Add elements for name label, overlay and overlay text elements to display participant information on top of the video streams.
1. Append all the video elements to the container element.

    ```js
    const remoteVideoContainerElm = document.getElementById('multistream-remote-video');
    
    function updateTheLayout(activeSpeakerVideoElems, memberVideoElems) {
      [...activeSpeakerVideoElems, ...memberVideoElems].forEach((videoElement) => {
        // Append all the video elements to the container element
        remoteVideoContainerElm.appendChild(videoElement);
      });
    }
    ```
