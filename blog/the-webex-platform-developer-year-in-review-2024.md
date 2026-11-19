---
type: Article
title: 'The Webex Platform Developer Year in Review: 2024'
canonical_url: https://developer.webex.com/blog/the-webex-platform-developer-year-in-review-2024
content_type: blog
date: '2025-01-29'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-webex-platform-developer-year-in-review-2024)

As we look back on 2024, it's clear that it has been a year of significant advancements and enhancements for the Webex platform. From new API features and SDK improvements to innovative service apps and streamlined identity management, Webex has continued to evolve to meet the needs of its users. In addition, we've added a variety of quality-of-life improvements as well as new content streams targeted at developers.

In this blog post, we'll explore the most notable updates and features introduced in 2024, highlighting how they can enhance your Webex experience and streamline your workflows.

### Guest-to-Guest Meetings

A Guest-to-Guest meeting is a type of Service App used in combination with a new subscription for guest-only meetings. The feature allows for guest accounts that are admin approved and can be either persistent or ephemeral. Additionally, the Guest-to-Guest Developer Sandbox is now available, providing a dedicated environment for developers to test and integrate guest meeting functionalities. For more information, see [Service App Guest-to-Guest Meetings](https://developer.webex.com/docs/service-apps-as-g2g-meeting-facilitator-guide).

### Webex Service Apps

Webex Service Apps are machine accounts that operate on behalf of an organization, independent of specific Webex user accounts. These apps are designed for your most critical and sensitive Webex integrations, making them an ideal solution for provisioning, active reporting, compliance, and more. They provide a robust and secure way to manage and automate various tasks within the Webex ecosystem. For more information, see [Using Webex Service Apps](https://developer.webex.com/docs/service-apps).

### Webex Calling API Update Highlights

Moving on to APIs, in 2024, the Webex Calling API saw numerous updates aimed at enhancing provisioning and management capabilities. Some of the key highlights include:

- **Ability to Add and Manage Virtual Lines**: Simplifies the process of handling virtual lines.
- **Ability to Manage Virtual Lines Call Settings**: Provides more control over call settings for virtual lines.
- **DECT Devices - Phase 2**: Expands support and functionality for DECT devices.
- **Device Configuration - Phase 3**: Further improvements in device configuration capabilities.
- **New Workspace Call Settings API**: Introduces new API for managing workspace call settings.
- **New Emergency Services API**: Adds support for emergency services management.
- **New Device API**: Enhances device management with a new API.
- **Enhanced PSTN Management**: Improves management of PSTN services.

For complete details, see [Webex Calling API Updates](https://developer.webex.com/docs/whats-new-calling).

#### Enhanced Call Reporting

The [Webex Calling Detailed Call History API](https://developer.webex.com/docs/api/v1/reports-detailed-call-history) was updated to include new fields that help customers identify PSTN provider details. These new fields include information such as PSTN Vendor Name and PSTN Legal Entity, providing more detailed insights into call history and improving overall call reporting capabilities.

#### New Converged Recordings APIs

In 2024, Webex introduced new [Converged Recordings APIs](https://developer.webex.com/docs/api/v1/converged-recordings) to streamline the management of call recordings. These APIs include:

- **List Recordings**: Retrieve a list of recordings.
- **List Recordings for an Admin or Compliance Officer**: Allow admins or compliance officers to list recordings.
- **Get Recording Details**: Fetch detailed information about a specific recording.
- **Delete a Recording**: Remove a recording from the system.
- **Get Recording Metadata**: Access metadata associated with a recording.
- **Reassign Recordings**: Reassign recordings to a different user.

These APIs provide comprehensive tools for managing recordings, enhancing administrative control and compliance capabilities.

### Webex Meetings API Update Highlights

The [Webex Meetings API](https://developer.webex.com/docs/meetings) introduced several new features to enhance meeting management and security:

- **Watermark Settings**: Meeting hosts can now add watermark settings by specifying new attributes:
  - `enabledAudioWatermark`
  - `enabledVisualWatermark`
  - `visualWatermarkOpacity`
- **Scheduling Options API**: Users can leverage this API to retrieve and update scheduling permissions on behalf of another user with the new parameter: `delegateEmails`.
- **Delegate Emails API**: Users can add and delete delegate emails, making it easier to manage scheduling permissions.
- **New Attributes for Meetings APIs**: These attributes help better manage registrations, post-event surveys for webinars, breakout sessions, and joined participants.

<br/>

### Other Notable Webex API Updates

We introduced several notable Webex API features that are designed to make administrators' lives easier. One of the highlights is the new [Identity Organization API](https://developer.webex.com/docs/api/v1/identity-organization), which enables administrators to manage organizational details more efficiently. With this API, admins can retrieve comprehensive details about their organization, including the current name, status, and other important information. Additionally, the new functionality allows admins to easily update the organization's name through a simple API call.

Another exciting update is the new [Reassign Recording API](https://developer.webex.com/docs/api/v1/converged-recordings/reassign-recordings). This feature allows administrators to reassign a list of call recordings or all call recordings of a particular user to a new user, streamlining the management of call recordings within the organization.

#### SCIM 2.0: Streamlined User Identity Management

The Webex platform enabled support for [the System for Cross-domain Identity Management (SCIM)](https://developer.webex.com/docs/scim-2-overview) v2.0 standard! With SCIM-enabled Webex APIs, you can easily configure or create SCIM 2.0 clients to manage users and groups. This automation simplifies the process of creating, updating, and deactivating user identities across applications, making identity management more efficient than ever.

One real-world use case for SCIM 2.0 is ISI Analytics, Directory Import for Webex, which provides the following benefits:

- Seamless Directory Integration for Webex
- Consistent, Up-to-Date Data
- Enhanced Insights with Full User Profiles

<br/>

### Webex SDKs

In 2024, we focused on enhancing our SDKs for both web and mobile platforms to provide developers with more powerful and flexible tools. These improvements include a migration to a new Meetings Suite platform, significant updates to the Webex Web Meetings SDK, and new features for the Webex Mobile SDKs for iOS and Android. These updates aim to enhance security, improve user experience, and offer greater control over media streams and meeting functionalities.

#### SDK Migration to New Meetings Suite Platform

We migrated our SDKs to a new Meetings Suite platform. This migration brought several advantages:

- **Unified Meeting Objects and Revised API Calls**: Simplifies the development process by providing a more consistent and streamlined API.
- **Enhanced Security**: Improves the overall security of meetings, ensuring that user data and communications are better protected.
- **Improved User Experience**: Offers a more intuitive and seamless experience for both developers and end-users, making it easier to integrate and use Webex functionalities.

<br/>

#### New in Webex Web Meetings SDK V3

The latest version of the [Webex Web Meetings SDK](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-introduction), V3, brings several exciting new features:

- **Stream Classes**: New classes for Camera, Mic, and Display, providing more control over media streams.
- **Effects**: Introduction of Background Noise Reduction and Virtual Background effects to enhance the meeting experience.
- **Transcription**: Support for Live Transcription and Multilanguage transcription, making meetings more accessible and inclusive.

Additionally, the SDK now supports [multistream](https://developer.webex.com/docs/multistream-comprehensive-guide), allowing users to receive multiple concurrent media streams with configurable layouts, rather than a single switched media stream with fixed layouts. This provides greater flexibility and a more customized meeting experience.

#### Mobile SDK Updates: iOS and Android SDK v3.1x

The latest updates to the Webex Mobile SDKs for [iOS](https://developer.webex.com/docs/sdks/ios) and [Android](https://developer.webex.com/docs/sdks/android) bring several new features:

- **Support for moving a user's meeting from one client to another**: This allows users to seamlessly transition their meetings between different devices.
- **Boost inbound call audio**: Enhances the audio quality for incoming calls.

For the iOS SDK only:

- **Support for iPad USB Camera for video calls**: Enables the use of external USB cameras with iPads for video calls.
- **Updated Kitchen Sink App with SwiftUI**: The Kitchen Sink App has been updated to use SwiftUI, providing a more modern and efficient user interface.

<br/>

### Webex Click-to-Call Apps

New [Click-to-Call functionality](https://developer.webex.com/docs/sdks/web-calling-sdk-click-to-call), allows users to contact a resource with a simple click. This feature streamlines communication by enabling instant connection to contacts directly from the Webex platform, enhancing productivity and ease of use.

### Webex Service Apps: Bring Your Own Datasource (BYODS)

The [Bring Your Own Datasource (BYODS)](https://developer.webex.com/docs/bring-your-own-datasource) feature for Webex Service Apps! This new capability streamlines development for Data Access Providers who want to manage Webex interaction data. It enhances real-time interactions within the Webex ecosystem and allows for direct exchanges between the Webex platform and data providers, making data management more seamless and efficient.

### Updated Webex Meeting Widget

[Webex Meeting Widget](https://developer.webex.com/docs/widgets) 1.28.0 made its debut. This update includes support for Node.js 20 and compatibility with React 18.3.1, making it easier than ever to enhance your web applications with Webex Meetings. In addition to this, the widget now supports providing the name for a guest as well as passwords or pins while joining meetings. A developer can also pass the name and password as inputs to the widget during initialization.

### Webex Developer AI Assistant

The Webex Developer AI Assistant is a cutting-edge tool designed to streamline the development process by providing intelligent code suggestions, automated documentation generation, and real-time debugging assistance for Webex APIs. This AI-powered assistant leverages advanced machine learning algorithms to enhance productivity and reduce development time, making it an invaluable resource for developers working with the Webex platform.



> **Info**
>
> You'll need to be logged into the Webex Developer Portal to see the new AI Assistant Beta button adjacent your profile.



### Webex Developer Playlist on YouTube

We started up the [Webex Developer Playlist on YouTube](https://www.youtube.com/playlist?list=PL2k86RlAekM_bIUrvVw4Haq_0xxTez9zU), featuring a curated collection of tutorials, demos, and deep dives into the latest Webex APIs and SDKs. This channel is designed to help developers get the most out of the Webex platform with easy-to-follow videos and expert insights.

### Many New Listings in the Webex App Hub

We added dozens of new apps to the Webex App Hub. To browse our new offerings, see [https://apphub.webex.com/brand-new](https://apphub.webex.com/brand-new).

### Discover App Hub Listings Natively in Webex

We're excited to announce that you can now discover App Hub listings directly within Webex! This means more visibility for your apps and bots without the need for context switching. Users can easily try out apps before adding them to their meetings or spaces, making the integration process smoother and more efficient:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1d890fcca2203617/2024-year-in-review-1.png)

### Looking Forward to 2025!

We've got even more ambitious plans for 2025 that we're looking forward to sharing with you in the coming months. Until then, best wishes for a great year!
