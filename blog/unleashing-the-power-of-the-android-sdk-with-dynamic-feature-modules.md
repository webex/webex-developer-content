---
type: Article
title: Unleashing the Power of the Android SDK with Dynamic Feature Modules
canonical_url: https://developer.webex.com/blog/unleashing-the-power-of-the-android-sdk-with-dynamic-feature-modules
content_type: blog
date: '2023-08-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/unleashing-the-power-of-the-android-sdk-with-dynamic-feature-modules)

In the ever-evolving landscape of Android development, two pivotal factors are reshaping the way we approach app creation and delivery. Firstly, Google Play Store now [sets a threshold](https://developer.android.com/guide/app-bundle#size_restrictions)—150 MB—as the maximum size for app uploads (per architecture). This directive not only encourages efficient app design but also underscores the significance of size-conscious development.

Adding to this paradigm shift is Android’s recommendation to utilize dynamic modules for larger applications. By adopting the app bundle format, you can tap into [Play Feature Delivery](https://developer.android.com/guide/playcore/feature-delivery), enabling the inclusion of feature modules that enhance your app based on conditions you define, like OnDemand download of modules later from Play Store.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt0ee1d170aa1d74a2/64e6763866f1ff414b2f5327/delivery.gif)

Moreover, we've cracked the code to seamlessly integrate the Webex SDK into dynamic modules. This breakthrough not only reduces app(.apk) size but also empowers you to leverage the dynamic compatibility of WebexSDK.

Let us begin the process 🚀📱.

### Prerequisites

To embark on this dynamic journey, make sure you have the following prerequisites in place:

- Android Studio setup:
  - Download Android Studio from [here](https://developer.android.com/studio)
  - Set up the environment for Android Studio.
- Knowledge of integrating with a Webex SDK. If you need guidance, refer to the following references:
  - [Requirements &amp; Feature List](https://developer.webex.com/docs/sdks/android)
  - [Guides](https://github.com/webex/webex-android-sdk/wiki)
  - [API Reference](https://webex.github.io/webex-android-sdk/)

Now that you are all set, let us dive into the exciting world of Android’s [Play Feature Delivery](https://developer.android.com/guide/playcore/feature-delivery), with WebexSDK.

### Step 1: Creating a Dynamic Feature Module

To kick off your dynamic adventure, follow these steps:

1. In Android Studio, select **File &gt; New &gt; New Module**  from the menu bar.
1. In the "**Create New Module**" dialog, choose **Dynamic Feature Module** and click **Next**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8e612f95de3a514d/64e6730037cf460af713c6cb/webexsdk-and-dynamic-feature-module-2.png)

1. Select the base module from the dropdown menu.
2. Provide a name and package name for your dynamic module and click **Next**.

    ![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltdb24a20b0978b222/64e673003026ee47da6b826c/webexsdk-and-dynamic-feature-module-3.png)

1. Give your module a catchy title. It's a good idea to use the same name you used when creating the module.
2. Select "**on-Demand only**" as the Install time inclusion.
3. If you want this module to be available to devices running Android 4.4 (API level 20) and lower, check the **Fusing**  box. This will include the module in multi-APKs.
4. Click **Finish**  to complete the setup. Now sit back and wait for Android Studio to finish the sync.

A [sample dynamic feature module](https://github.com/webex/webex-android-sdk-example/tree/Alpha/3.9.0/app) for the reference

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltddbd99ba6501cbc9/64e6730037cf4652b213c6cf/webexsdk-and-dynamic-feature-module-4.png)

### Step 2: Configuring the Webex Android SDK in the Dynamic Feature Module

Configuring the Webex Android SDK within your dynamic feature module is a crucial step that ensures seamless integration of collaboration capabilities. This configuration bridges the gap between your base and dynamic modules, enabling them to work harmoniously.

#### Dynamic Feature Module: build.gradle

Let us make sure the IDE has applied the configuration correctly. Open the dynamic feature module's [build.gradle](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/dynamicfeature/build.gradle) file and ensure the following:

- The `com.android.dynamic-feature` plugin is added.
- Remove unnecessary configurations such as `signing configurations`, `minifyEnabled`, `versionCode`, `versionName`, and app’s `meta-data`.
- Add the [WebexSDK](https://github.com/webex/webex-android-sdk/releases/tag/3.9.2) dependency for the dynamic module: `implementation 'com.ciscowebex:webexsdk-wxc:3.9.2'`

<br/>

#### Dynamic feature module: AndroidManifest.xml

Define on-demand module attributes with split name, title, and on-demand availability in [AndroidManifest.xml](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/dynamicfeature/src/main/AndroidManifest.xml)

- Use `dist:module` for packaging and distribution settings.
- Specify `dist:OnDemand:` for on-demand download.
- Use `dist:fusing` to include the module in lower Android versions.
- Set `android:hasCode` to false if no DEX files to avoid runtime errors.

<br/>

#### Base module: build.gradle

- Verify IDE applied configuration with `android.dynamicFeatures = [":dynamicfeature"]`.
- For reusable dependencies use the API keyword, while defining dependencies.
- Add play core library for dynamic feature support.
- Set `applicationId`, `minSdk`, `targetSdk`, `versionCode`, and `versionName`.

Full configs for gradle files can be seen [here](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/build.gradle).

Now let us visualize the Collaboration of base and dynamic modules with dependency! 🧐😎.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt342608df039f0ebb/64e6730056ef58b7868ee594/webexsdk-and-dynamic-feature-module-5.png)

#### Base module: AndroidManifest.xml

To **enable WebexSDK to collect logs** in the SD card at the directory: `/sdcard/Android/data/<app-id>/cache/logs`, the base module should define a [file provider for the SDK](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/src/main/AndroidManifest.xml#L100) in its [manifest](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/src/main/AndroidManifest.xml). It is important to note that, as per the bundling rules, dynamic module providers are not visible to the base module during compilation time.



> **Info**
>
> Including the above entry in the base module resolves manifest merge issues for the `WebexSdkFileProvider` in the WebexSDK library. Compiler adds the entry at runtime, so ignore Android Studio errors while adding the snippet. Manifest merger handles the conflict during project build..



#### Request an OnDemand Module

When your app needs to use a feature module, it can request one while it’s in the foreground through the [SplitInstallManager](https://developer.android.com/reference/com/google/android/play/core/splitinstall/SplitInstallManager) class. When making a request, your app needs to specify the name of the module as defined by the [split](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/dynamicfeature/src/main/AndroidManifest.xml#L6) element in the target module’s manifest. When you create a feature module using Android Studio, the build system uses the Module name you have provided, to inject this property into the module’s manifest at compile time.



> **Info**
>
> To have access to the module’s code and resources, your app needs to enable  [SplitCompat](https://developer.android.com/guide/playcore/feature-delivery/on-demand#access_downloaded_modules).



#### Handle dynamic module download states

Now we need to manage the installation request and monitor the status of the [dynamic module](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/src/main/java/com/ciscowebex/androidsdk/kitchensink/base/SplashActivity.kt#L41) download using the [SplitInstallStateUpdatedListener](https://developer.android.com/reference/com/google/android/play/core/splitinstall/SplitInstallStateUpdatedListener).

```java
SplitInstallStateUpdatedListener listener = state -> 
{
  if (state.status() == SplitInstallSessionStatus.FAILED 
    && state.errorCode() == SplitInstallErrorCode.SERVICE_DIES) {
    // Retry the request.
    return;
  }
  switch (state.status()) {
    case SplitInstallSessionStatus.DOWNLOADING:
      // Update progress bar.
      break;
    case SplitInstallSessionStatus.INSTALLED:
      //Module is downloaded successfully
      break;
  }
};
…
…

// Registers the listener.
installManager.registerListener(listener);
installManager.startInstall(request)
```

For error details, refer [here](https://developer.android.com/reference/com/google/android/play/core/splitinstall/model/SplitInstallErrorCode).

#### Managing dynamic feature modules:

Cancel a module installation request before installation with: <br/>
`splitInstallManager.cancelInstall(sessionId)`.

Check currently installed dynamic feature modules on the device with: <br/> 
`Set<String>installedModules = splitInstallManager.getInstalledModules()`.

Uninstall modules using: <br/>
`splitInstallManager.deferredUninstall(Arrays.asList("moduleName"))`.

Launching the Webex Module after Successful Installation:
- `LoginActivity` - In the dynamic module, create a [`LoginActivity`](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/dynamicfeature/src/main/java/com/ciscowebex/androidsdk/kitchensink/auth/LoginActivity.kt) which acts as the gateway to the dynamic module and Webex SDK.
- `SplitCompat.install(context)` is to be defined for all the activity components of dynamic module.
- After a successful dynamic module installation, call [`launchActivity()`](https://github.com/webex/webex-android-sdk-example/blob/Alpha/3.9.0/app/src/main/java/com/ciscowebex/androidsdk/kitchensink/base/SplashActivity.kt#L158) with the class name from the base module.

<br/>

### 🚨 Important Notes: Android Dynamic Module Integration 🚨

When it comes to Android Dynamic Module integration, we must address a significant challenge: the base module's inability to directly utilize code from the dynamic module. Fear not, we have some smart solutions to conquer this hurdle:

- **Communication through Interfaces:** Create interfaces in the base module that the dynamic module can implement. This clever approach enables smooth communication and code usage between the two modules.
- **Reflection Magic:** Embrace the power of reflection! Utilize it to access the dynamic module's code indirectly from the base module. Although it comes with a performance cost, it gets the job done.
- **Shared Libraries:** Unite code forces! Extract common code into shared libraries that both the base and dynamic modules can depend on. This fosters code reuse and simplifies inter-module communication.

By implementing these genius solutions, you'll master the art of seamless integration and collaboration between the base and dynamic modules.

### Conclusion

In the realm of Android app development, Google Play's 150 MB cap pushes efficient design. Dynamic modules enrich larger apps, while our Webex SDK integration optimizes size and enhances capabilities. Achieve a balance of efficiency and collaboration, empowering your app's success.

Happy coding and keep building amazing apps! 🤩💻📲
