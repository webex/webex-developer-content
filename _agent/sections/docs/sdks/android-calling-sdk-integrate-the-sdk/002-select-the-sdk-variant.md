---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Select the SDK Variant
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-integrate-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Android SDK v3.16+ Permission Behavior Changes](003-android-sdk-v3-16-permission-behavior-changes.md)

## Article introduction

The Webex Android SDK is available through Maven. Follow the instructions below to integrate the SDK into your application.

## Selected section

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
