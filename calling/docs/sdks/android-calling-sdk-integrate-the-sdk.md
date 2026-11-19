---
type: Guide
title: Android Calling SDK | Integrate the SDK
display_title: Integrate the SDK
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk
content_type: documentation
product_group:
- webex-suite
categories:
- calling
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk)

The Webex Android SDK is available through Maven. Follow the instructions below to integrate the SDK into your application.

## Add the Maven Repository

> **Maven repository URL migration:** The Android SDK Maven repository URL has changed from `devhub.cisco.com` to `arti.anon.devhub-cloud.cisco.com`. Update your project-level Gradle configuration before performing a clean build or resolving SDK versions. Changing the repository URL alone does not require changing the SDK variant. This guide also updates the Full SDK and Webex-Wxc examples from version `3.16.3` to `3.17.0`. If your organization uses repository allowlists or network proxies, allow the new domain.

Insert the following Maven repository into your project-level `build.gradle`:

```groovy
allprojects {
    repositories {
        maven {
            url 'https://arti.anon.devhub-cloud.cisco.com/artifactory/webexsdk/'
        }
    }
}
```

## Select the SDK Variant

The Mobile Android SDK is available in two variants:

* **Webex-Wxc SDK**: Optimized for size. Suitable if your app only uses Webex Calling.
* **Full SDK**: Includes meetings, messaging, and supports UCM calling along with Webex Calling.

### Use the Full SDK

In your module-level `build.gradle`, add the **Full SDK** as a dependency:

```groovy
dependencies {
    implementation 'com.ciscowebex:webexsdk:3.17.0'
}
```

### Use the Webex-Wxc SDK

In your module-level `build.gradle`, add the size-optimized Webex-Wxc SDK as a dependency:

```groovy
dependencies {
    implementation 'com.ciscowebex:webexsdk-wxc:3.17.0'
}
```

## Android SDK v3.16+ Permission Behavior Changes

From Android SDK v3.16 onwards, runtime permission handling is app-owned:

* The SDK does not include dangerous permissions in the library manifest.
* The SDK does not show permission dialogs.
* Your app must declare required permissions and request them at runtime before SDK operations.
* If permissions are missing, SDK APIs return `WebexError.ErrorCode.PERMISSION_REQUIRED` and include missing permissions in `error.data`.

The SDK also includes support for 16 KB memory page size on Android; no app code change is required for that part.

### Common calling permissions

```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
```

### Runtime permission check example

```kotlin
val required = listOf(Manifest.permission.RECORD_AUDIO)
val missing = required.filter {
    ContextCompat.checkSelfPermission(ctx, it) != PackageManager.PERMISSION_GRANTED
}

if (missing.isNotEmpty()) {
    // requestPermissions(missing.toTypedArray(), REQ_CODE)
    return
}

webex.phone.dial(address, MediaOption.audioOnly()) { result ->
    // Handle result. If permission is missing, SDK returns PERMISSION_REQUIRED.
}
```
