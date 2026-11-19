---
type: Article
title: 'Announcing the Webex Mobile SDK 3.15: Introducing the Messaging Only SDK'
canonical_url: https://developer.webex.com/blog/announcing-the-webex-mobile-sdk-3-15-introducing-the-messaging-only-sdk
content_type: blog
date: '2025-03-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/announcing-the-webex-mobile-sdk-3-15-introducing-the-messaging-only-sdk)

We are excited to announce the release of Webex Mobile SDK version 3.15, featuring our new Messaging Only SDK for both [iOS](https://developer.webex.com/docs/sdks/ios) and [Android](https://developer.webex.com/docs/sdks/android)! This innovation is designed to cater to developers and businesses looking to integrate Webex's powerful messaging capabilities into their mobile applications without the additional features of calling and meetings.

### Why Choose the Messaging Only SDK?

By focusing solely on messaging, the new SDK variant offers a streamlined solution that not only optimizes performance but also reduces the overall size of the SDK. This is particularly beneficial for industries like banking, where secure and reliable messaging is a priority.

By isolating the messaging component, developers can seamlessly integrate Webex's robust messaging features into their mobile apps. With a smaller SDK size, applications can achieve better performance and reduced resource consumption.

### How to Use and Implement the Messaging Only SDK

Integrating the Messaging Only SDK into your mobile applications is straightforward. Below are the steps for both iOS and Android platforms:

#### iOS Integration

To create the iOS integration:

1. Add the Messaging Only SDK to your Podfile to include it in your project:

    ```bash
    target 'MyApp' do
    pod 'WebexSDK/Message', '~&gt; 3.15.0'
    end
    ```

1. Run the following command in your terminal to install the SDK:

    ```bash
    pod install
    ```

1. Import and initialize the SDK in your application code:

    ```swift
    import WebexSDK

    // Initialize Webex messaging
    let webex = Webex(authenticationStrategy: yourAuthStrategy)
    ```

1. Implement Messaging Features

Utilize the [provided APIs](https://webex.github.io/webex-ios-sdk/) to send, receive, and manage messages as per your application's requirements. The [SDK documentation](https://webex.github.io/webex-ios-sdk/) includes detailed examples to guide you through these processes.

#### Android Integration

To create the Android integration:

1. Download the [WebexSDK-Message.aar](https://github.com/webex/webex-android-sdk/releases/download/3.15.0/WebexSDK-Message.aar) file and include it in your project's libs directory.
1. Add the following to your `build.gradle` file to ensure the SDK is included in your build process:

    ```text
    allprojects {
        repositories {
            jcenter()
            maven {
                url 'https://devhub.cisco.com/artifactory/webexsdk/'
            }
        }
    }
    dependencies {
        implementation 'com.ciscowebex:webexsdk-message:3.15.0'
    }
    ```

1. Import and initialize the SDK in your application code:

    ```java
    import com.cisco.webex.androidsdk.Webex;

    // Initialize Webex messaging
    Webex webex = new Webex(yourAuthStrategy);
    ```

1. Utilize the [provided APIs](https://webex.github.io/webex-android-sdk/dokka-docs/com.ciscowebex.androidsdk.message/index.html) to send, receive, and manage messages as per your application's requirements. The [SDK documentation](https://webex.github.io/webex-android-sdk/dokka-docs/com.ciscowebex.androidsdk.message/index.html) includes detailed examples to guide you through these processes.

<br/>

### Conclusion

The release of the Messaging Only SDK in version 3.15 marks a significant step forward in our commitment to providing versatile and efficient communication solutions. By focusing on the essential messaging features, we can offer a product that meets the specific needs of our customers, facilitating enhanced communication and collaboration.

Stay tuned for more updates and enhancements as we continue to innovate and expand our offerings to meet the diverse needs of our users.

We look forward to seeing how you leverage the new Messaging Only SDK in your projects. For any questions or support, feel free to reach out to our [developer community](https://cs.co/WebexDeveloperCommunity) or contact us [directly](https://developer.webex.com/support). Happy coding!
