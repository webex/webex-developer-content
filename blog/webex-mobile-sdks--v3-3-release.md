---
type: Article
title: Webex Mobile SDKs - v3.3 Release
canonical_url: https://developer.webex.com/blog/webex-mobile-sdks--v3-3-release
content_type: blog
date: '2022-03-21'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-mobile-sdks--v3-3-release)

The Webex iOS and Android SDKs recent v3.3 release has a diverse set of features that satisfy several use cases for customers within healthcare, field services, education, and more. The v3.3 update includes features that enables developers to receive real time transcripts of Webex meetings, access enhanced resolution controls for screen sharing and photos taken during Webex meetings and provides additional control over the mobile device camera options and configurations.

### Real-time transcripts

Transcription has many use cases around compliance, accessibility, just-in-time knowledge discovery, and more. Following a recent update to the JavaScript SDK that provided the ability to receive the meeting’s [real time transcripts](https://developer.webex.com/blog/webex-javascript-sdk-now-has-real-time-meeting-transcription), Webex is releasing the same feature for the Mobile SDKs to provide cohesive experience across all applications no matter the platform. What differentiates Webex transcription services is that we do not only do transcription of the audio exchanged during the meeting, but we also leverage AI to enhance the accuracy of the transcribed speech and thus ensure the highest possible transcription accuracy delivered to end users. The feature is available for Webex meetings where [Webex Assistant](https://help.webex.com/en-us/article/ygksov/Webex-Assistant-for-Webex-Meetings) is available, for scheduled meetings and Personal meeting rooms (PMRs), and for [licensed users](https://help.webex.com/en-us/article/6qoekm/Add-Licenses-for-Webex-Assistant-for-Webex-Meetings). In addition to the ability to receive transcripts live during meetings, the SDKs provide the developers with the ability to enable and disable the Webex Assistant. Transcripts also are provided with metadata such as speaker name and timestamp for better tracking and alignment with the audio being transcribed.

### Additional resolution controls

Envision a participant trying to zoom in to view a shared document during a Webex meeting. This user can be a student, a field technician, or any other. If the user is running the application on a small screen such as a mobile device or even a wearable, the resolution must be high enough to allow the user to zoom in without resolution degradation. In the v3.3 update, we are enhancing the SDKs to allow developers to leverage higher screen share resolutions when receiving the shared content. Webex supports resolutions up to 4K (Ultra High Definition, UHD), subject to the recipient network quality.

Perhaps a healthcare provider is meeting virtually with a patient and decides during the meeting to take a photo of the patient’s symptom to share it with a colleague for consultation or keep it for future records. Given the fact that mobile devices’ cameras have evolved dramatically and support very high resolutions when taking photos, our SDKs have been enhanced to allow developers to leverage the highest photo resolution their mobile devices cameras can support when taking photos during Webex meetings.

### Additional camera controls

One of the main pain-points developers face today is not being able to access the native OS APIs of the mobile device’s camera during a running meeting. This is because the running meeting controls the camera for transmitting the video streams. In this release, additional controls for the camera object during a running Webex meeting are provided. Developers will be able to control:

- Setting the Zoom In/Out factor
- Setting flashlight mode On/Off
- Setting the camera’s flash when taking a photo
- Adjusting camera exposure
- Controlling the camera’s focus on specific coordinates

&nbsp;

### Getting Started

There are plenty of resources to help our developers to start using the Webex Mobile SDKs in general or the new features in the v3.3 update. For some examples, see:

- [Webex iOS SDK example](https://github.com/webex/webex-ios-sdk-example)
- [Webex Android SDK example](https://github.com/webex/webex-android-sdk-example)
- [Real-time transcription API starter](https://github.com/webex/webex-ios-sdk/wiki/Real-time-Transcription-APIs)
- [Advanced camera options guide for iOS](https://github.com/webex/webex-ios-sdk/wiki/Advanced-Camera-APIs)
- [Advanced camera options for Android](https://github.com/webex/webex-android-sdk/wiki/Camera-APIs)

&nbsp;

### Your Feedback Matters

If you have feedback, suggestions, or you are encountering issues using the REST APIs, please reach out to our support team [https://developer.webex.com/support](https://developer.webex.com/support), and we will be happy to help! In addition, feel free to post questions (and answers!) in our new [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers).
