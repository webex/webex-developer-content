---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-integrating-the-sdk
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the Maven Repository
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-meetings-sdk-integrating-the-sdk). [Full Markdown](../../../../../docs/sdks/android-meetings-sdk-integrating-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Android SDK v3.16+ Permission Behavior Changes](002-android-sdk-v3-16-permission-behavior-changes.md)

## Article introduction

Whether you need the full SDK for comprehensive features or a size-optimized version for meeting flows only, this article will help you set up the necessary dependencies.

## Selected section

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
