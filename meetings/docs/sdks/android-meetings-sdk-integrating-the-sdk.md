---
type: Guide
title: Android Meetings SDK | Integrating the SDK
display_title: Integrating the SDK
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-integrating-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-integrating-the-sdk)

Whether you need the full SDK for comprehensive features or a size-optimized version for meeting flows only, this article will help you set up the necessary dependencies.

## Add the Maven Repository

> **Maven repository URL migration:** The Android SDK Maven repository URL has changed from `devhub.cisco.com` to `arti.anon.devhub-cloud.cisco.com`. Update your project-level Gradle configuration before performing a clean build or resolving SDK versions. Changing the repository URL alone does not require changing the SDK dependency. This guide also updates the Full SDK and Meetings SDK examples from version `3.16.3` to `3.17.0`. If your organization uses repository allowlists or network proxies, allow the new domain.

The Webex Android SDK is distributed via maven. To integrate the SDK into your app, you need to add the following dependency to your app's `build.gradle` file:

1. Add the following repository to your top-level `build.gradle` file:

    ```groovy
    allprojects {
        repositories {
            maven {
                url 'https://arti.anon.devhub-cloud.cisco.com/artifactory/webexsdk/'
            }
        }
    }
    ```

1. The Android meetings SDK comes in two variants. If your use case involves only meeting flows, consider using the size-optimized Meeting SDK. If you need features beyond meetings, you will need to use the full SDK.

    Add the required `webexsdk` library as a dependency for your app in the `build.gradle` file:

    * For the full SDK:

        ```groovy
        dependencies {
            implementation 'com.ciscowebex:webexsdk:3.17.0'
        }
        ```

    * For the meetings only SDK:

        ```groovy
        dependencies {
            implementation 'com.ciscowebex:webexsdk-meeting:3.17.0'
        }
        ```

## Android SDK v3.16+ Permission Behavior Changes

From Android SDK v3.16 onwards, runtime permission handling is app-owned:

* The SDK does not include dangerous permissions in the library manifest.
* The SDK does not show permission dialogs.
* Your app must declare required permissions and request them at runtime before SDK operations.
* If permissions are missing, SDK APIs return `WebexError.ErrorCode.PERMISSION_REQUIRED` and include missing permissions in `error.data`.

The SDK also includes support for 16 KB memory page size on Android; no app code change is required for that part.

### Common meetings permissions

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
```

### Runtime permission check example

```kotlin
val needed = arrayOf(Manifest.permission.RECORD_AUDIO, Manifest.permission.CAMERA)
// request missing permissions before dial/answer
webex.phone.dial(address, MediaOption.audioVideo(/* views */)) { result ->
    // Handle result. If permission is missing, SDK returns PERMISSION_REQUIRED.
}
```

### Screen-sharing consent flow

For screen sharing, obtain MediaProjection user consent and pass the consent data into `startSharing(...)`:

```kotlin
val mgr = ctx.getSystemService(Context.MEDIA_PROJECTION_SERVICE) as MediaProjectionManager
val consentIntent = mgr.createScreenCaptureIntent()
launcher.launch(consentIntent)
// In activity result callback:
call.startSharing(notification, notifId, data /* consent */, callback, shareConfig)
```
