---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Add the Maven Repository
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/android-calling-sdk-integrate-the-sdk). [Full Markdown](../../../../../docs/sdks/android-calling-sdk-integrate-the-sdk.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Android SDK v3.16+ Permission Behavior Changes](003-android-sdk-v3-16-permission-behavior-changes.md)

## Article introduction

The Webex Android SDK is available through Maven. Follow the instructions below to integrate the SDK into your application.

## Selected section

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
