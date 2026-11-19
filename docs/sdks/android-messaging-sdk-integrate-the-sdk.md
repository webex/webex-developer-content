---
type: Guide
title: Android Messaging SDK | Integrate the SDK
display_title: Integrate the SDK
canonical_url: https://developer.webex.com/docs/sdks/android-messaging-sdk-integrate-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- messaging
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-messaging-sdk-integrate-the-sdk)

The Webex Android Messaging SDK is distributed via Maven. This article explains the steps necessary to add the SDK to your own Android app.

## Add the Maven Repository

> **Maven repository URL migration:** The Android SDK Maven repository URL has changed from `devhub.cisco.com` to `arti.anon.devhub-cloud.cisco.com`. Update your project-level Gradle configuration before performing a clean build or resolving SDK versions. Changing the repository URL alone does not require changing the SDK artifact. This guide also switches the example to the messaging-only artifact, `com.ciscowebex:webexsdk-message:3.17.0`. If your organization uses repository allowlists or network proxies, allow the new domain.

To integrate the Webex Android Messaging SDK into your app:

1. Add the following **repository** to your top-level `build.gradle` file:

    ```groovy
    allprojects {
        repositories {
            maven {
                url 'https://arti.anon.devhub-cloud.cisco.com/artifactory/webexsdk/'
            }
        }
    }
    ```

2. Add the following **dependency** for your app in the app `build.gradle` file:

    ```groovy
    dependencies {
        implementation 'com.ciscowebex:webexsdk-message:3.17.0'
    }
    ```
