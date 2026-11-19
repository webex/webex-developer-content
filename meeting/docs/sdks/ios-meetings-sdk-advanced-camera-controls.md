---
type: Guide
title: iOS Meetings SDK | Advanced Camera Controls
display_title: Advanced Camera Controls
canonical_url: https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/ios-meetings-sdk-advanced-camera-controls)

The iOS Meetings SDK provides methods that let you have enhanced control over the device's system camera. Users can adjust exposure values, set the zoom factor, manage the camera torch, and more.

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

```swift
var cameraTorchMode: TorchMode
```

![Torch](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt8428c7facee51d39/torch.gif)

## Camera Flash Mode

Control the camera flash that activates during the `takePhoto()` method call:

```swift
var cameraFlashMode: FlashMode
```

![Flash](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2f59449bd39266dd/Flash.gif)

## Video Zoom Factor

Allows zooming based on the device's capabilities:

```swift
var zoomFactor: Float
```

![Zoom](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7d23195671b93f56/zoom.gif)

## Camera Exposure Duration

Retrieve the minimum, maximum, and current camera exposure duration values. Default is 0 until set:

```swift
var exposureDuration: CameraExposureDuration
```

## Camera Exposure ISO

Obtain the minimum, maximum, and current camera exposure ISO values. Default is 0 until set:

```swift
var exposureISO: CameraExposureISO
```

## Camera Exposure Target Bias

Get the minimum, maximum, and current values of the camera's target bias. Default is 0 until set:

```swift
var exposureTargetBias: CameraExposureTargetBias
```

## Camera Focus at Point

Focus the camera at a specific X and Y coordinate:

```swift
func setCameraFocusAtPoint(pointX: Float, pointY: Float) -> Bool
```

![Focus Point](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt59db822471f14e56/FocusPoint.gif)

## Custom Camera Exposure

Adjust exposure manually with a specific duration and ISO. Exposure duration determines the amount of time your film is exposed to light when taking a photograph. ISO refers to your camera's sensitivity to light, whether it pertains to film or a digital sensor. A lower ISO value means less sensitivity to light, while a higher ISO means more sensitivity.

```swift
func setCameraCustomExposure(duration: UInt64, iso: Float) -> Bool
```

![Duration and ISO](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt2fbb4b6efe80e2ba/DurationISO.gif)

## Camera Auto Exposure

Automatically adjust exposure based on the target bias value:

```swift
func setCameraAutoExposure(targetBias: Float) -> Bool
```

![Target Bias](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd9d3807ba067dc4e/TargetBias.gif)

## Take a Photo

Capture a photo from the local view. The photo data is returned as a byte array:

```swift
func takePhoto() -> Bool
```

```swift
Call.onPhotoCaptured: ((_ imageData: Data?) -> Void)?
```

![Take a Photo](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf54c07a53d1b6e6f/takephoto.gif)
