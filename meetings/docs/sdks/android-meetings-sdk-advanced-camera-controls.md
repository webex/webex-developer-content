---
type: Guide
title: Android Meetings SDK | Advanced Camera Controls
display_title: Advanced Camera Controls
canonical_url: https://developer.webex.com/docs/sdks/android-meetings-sdk-advanced-camera-controls
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/android-meetings-sdk-advanced-camera-controls)

The Android Meetings SDK provides methods that let you have enhanced control over the device's system camera. Users can adjust exposure values, set the zoom factor, manage the camera torch, and more.

---



> **Info**
>
> Available starting from SDK version 3.3.0 and later.



## Important Notes

Before using the advanced camera methods:

1. Ensure you are in a call, either 1-1 or within a meeting.
2. Enable the local camera view to access camera methods.
3. Invoke the desired camera methods.

## Camera Torch Mode

Enable, disable, or auto-enable the camera torch (flashlight). Applicable only to the rear camera:

```kotlin
setCameraTorchMode(mode: TorchMode)
```

![Torch](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt01ca54d1163b67b0/torch.gif)

## Camera Flash Mode

Control the camera flash that activates during the `takePhoto()` method call:

```kotlin
setCameraFlashMode(mode: FlashMode)
```

![Control the flash](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2849f9b986d2c503/flash_takephoto.gif)

## Video Zoom Factor

Allows zooming based on the device's capabilities:

```kotlin
setVideoZoomFactor(factor: Float)
```

![Zoom factor](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt90ed3e429d9eee72/zoom.gif)

## Camera Exposure Duration

Retrieve the minimum, maximum, and current camera exposure duration values. Default is 0 until set:

```kotlin
getCameraExposureDuration(): CameraExposureDuration
```

## Camera Exposure ISO

Obtain the minimum, maximum, and current camera exposure ISO values. Default is 0 until set:

```kotlin
getCameraExposureISO(): CameraExposureISO
```

## Camera Exposure Target Bias

Get the minimum, maximum, and current values of the camera's target bias. Default is 0 until set:

```kotlin
getCameraExposureTargetBias(): CameraExposureTargetBias
```

## Camera Focus at Point

Focus the camera at a specific X and Y coordinate:

```kotlin
setCameraFocusAtPoint(pointX: Float, pointY: Float)
```

## Custom Camera Exposure

Adjust exposure manually with a specific duration and ISO. Exposure duration determines the amount of time your film is exposed to light when taking a photograph. ISO refers to your camera's sensitivity to light, whether it pertains to film or a digital sensor. A lower ISO value means less sensitivity to light, while a higher ISO means more sensitivity.

```kotlin
setCameraCustomExposure(duration: Double, iso: Float)
```

![Custom Exposure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9ad1bc82ea8de52c/customexposure.gif)

## Camera Auto Exposure

Automatically adjust exposure based on the target bias value:

```kotlin
setCameraAutoExposure(targetBias: Float)
```

![Auto Exposure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt106bd2e3d928c53a/autoexposure.gif)

## Take a Photo

Capture a photo from the local view. The photo data is returned as a byte array:

```kotlin
takePhoto()
```

```kotlin
fun onPhotoCaptured(imageData: ByteArray?)
```

![Take a Photo](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt08c200753e3270ff/takephoto.gif)
