---
type: Guide
title: Web Meetings SDK | Streams and Effects
display_title: Streams & Effects
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
content_type: documentation
product_group:
- webex-suite
categories:
- meeting
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects)

The Webex Meetings Web SDK version 3.0 introduces new APIs designed to facilitate the management of local media streams for audio, video, and screen sharing. This article explains how the `Streams` object functions with two newly added effects: `VirtualBackgroundEffect` and `NoiseReductionEffect`. Those effects and their corresponding methods are available in the plugin-meetings package.

---



> **Info**
>
> See the [kitchen sink app](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings) for examples of the effects.



## Streams

The following new `Streams` classes have been introduced:

1. [LocalCameraStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-camera-stream.ts)
2. [LocalMicrophone](https://github.com/webex/webrtc-core/blob/main/src/media/local-microphone-stream.ts)
3. [LocalDisplayStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-display-stream.ts)
4. [LocalSystemAudioStream](https://github.com/webex/webrtc-core/blob/main/src/media/local-system-audio-stream.ts)


Import the `Streams` classes into your applications using the `plugin-meetings` package:

```js
import {
  LocalCameraStream,
  LocalMicrophoneStream,
  LocalDisplayStream,
  LocalSystemAudioStream,
  createCameraStream,
  createMicrophoneStream,
  createDisplayStream,
  createDisplayStreamWithAudio
} from '@webex/plugin-meetings';
```

## Create Streams

To create a stream, camera, microphone, or display, invoke the respective method while passing any required parameters:

```js
const cameraStream = await createCameraStream(cameraConstraints);

const microphoneStream = await createMicrophoneStream(audioConstraints);

const [localShareVideoStream, localShareAudioStream] = await createDisplayStreamWithAudio();
```

Here are the supported constraints:

```js
const cameraConstraints = {
    deviceId?: ConstrainDOMString;
    width?: ConstrainULong;
    height?: ConstrainULong;
    aspectRatio?: ConstrainDouble;
    frameRate?: ConstrainDouble;
    facingMode?: ConstrainDOMString;
};

const audioConstraints = {
    deviceId?: string;
    autoGainControl?: boolean;
    echoCancellation?: boolean;
    noiseSuppression?: boolean;
};
```

## Virtual Background Effect

The virtual background can take the form of an image, an MP4 video, or a user's actual background with an applied blur. The blur option offers additional flexibility including adjustable strength and quality levels.



> **Info**
>
> Higher blur settings will put a greater computational demand on your computer.



Use the `Meetings` object's `createVirtualBackgroundEffect()` method to apply effects:

```js
await webex.meetings.createVirtualBackgroundEffect(options);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td>
        <strong>Asynchronous</strong>
      </td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>
        <strong>Parameters</strong>
      </td>
      <td>
        options
        
          <table>
            <tbody>
              <tr>
                <th><strong>Name</strong></th>
                <th><strong>Description</strong></th>
                <th><strong>Values</strong></th>
                <th><strong>Required</strong></th>
              </tr>
              <tr>
                <td><code>generator</code></td>
                <td>
                  Determines where the model runs (on the main thread or a background thread).
                </td>
                <td>
                  string
                  
                    <table>
                      <tbody>
                        <tr>
                          <td>
                            <code>local</code>
                          </td>
                          <td>
                            <code>worker</code>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Optional. Defaults to<code>worker</code>.
                </td>
              </tr>
              <tr>
                <td><code>frameRate</code></td>
                <td>
                  Determines how many frames are sent to the model per
                    second.
                </td>
                <td>
                    <code>number</code>
                  
                    <table>
                      <tbody>
                        <tr>
                          <td>0-60</td>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Optional. Defaults to <code>30</code>.
                </td>
              </tr>
              <tr>
                <td><code>quality</code></td>
                <td>
                  Determines the accuracy of the model (higher accuracy
                    requires additional CPU resources).
                </td>
                <td>
                  string
                  
                    <table>
                      <tbody>
                        <tr>
                          <code>LOW</code>, 
                          <code>MEDIUM</code>, 
                          <code>HIGH</code>, 
                          <code>ULTRA</code>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Optional. Defaults to <code>LOW</code>.
                </td>
              </tr>
              <tr>
                <td><code>mirror</code></td>
                <td>
                  Whether the output image should be flipped
                    horizontally.
                </td>
                <td>
                  boolean
                </td>
                <td>
                  Optional. Defaults to <code>false</code>.
                </td>
              </tr>
              <tr>
                <td><code>mode</code></td>
                <td>
                  Determines the type of background to render behind a
                    user.
                </td>
                <td>
                  string
                  
                    <table>
                      <tbody>
                        <tr>
                          <code>BLUR</code>, 
                          <code>IMAGE</code>, 
                          <code>VIDEO</code>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Optional. Defaults to <code>BLUR</code>.
                </td>
              </tr>
              <tr>
                <td><code>blurStrength</code></td>
                <td>
                  Determines how strongly the background is blurred.
                </td>
                <td>
                  string
                  
                    <table>
                      <tbody>
                        <tr>
                          <code>WEAK</code>, 
                          <code>MODERATE</code>, 
                          <code>STRONG</code>, 
                          <code>STRONGER</code>, 
                          <code>STRONGEST</code>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Required in <code>BLUR</code>mode. Defaults to STRONG.
                </td>
              </tr>
              <tr>
                <td><code>bgImageUrl</code></td>
                <td>
                 Path to a background image that replaces the original
                    background.
                </td>
                <td>
                  String Fully qualified URL.
                </td>
                <td>
                  Required in <code>IMAGE</code>mode.
                </td>
              </tr>
              <tr>
                <td><code>bgVideoUrl</code></td>
                <td>
                 Path to a background video that replaces the original
                    background.
                </td>
                <td>
                  String. Fully qualified URL (MP4 only).
                </td>
                <td>
                  Required in <code>VIDEO</code>mode
                </td>
              </tr>
              <tr>
                <td><code>preventBackgroundThrottling</code></td>
                <td>
                 If set to <code>true</code>, prevents the browser from throttling the effect frame rate when the page is hidden.
                </td>
                <td>
                  <code>true</code>, <code>false</code>
                </td>
                <td>
                  Defaults to <code>false</code>.
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        <strong>Returns</strong>
      </td>
      <td colspan="1">
        A promise that returns the virtual background effect.
      </td>
    </tr>
  </tbody>
</table>

## Apply a Virtual Background Effect

To apply a virtual background effect to your camera `Stream`:

1. Create a local camera stream with any desired constraints:

   ```js
   const cameraConstraints = { width: 640, height: 480 };

   const cameraStream = await createCameraStream(cameraConstraints);
   ```

2. Add the camera stream to the video `srcObject`:

   ```js
   meetingStreamsLocalVideo.srcObject = cameraStream.outputStream;
   ```

3. Create the virtual background effect using the `createVirtualBackgroundEffect()` method:

   ```js
   const effect = await webex.meetings.createVirtualBackgroundEffect();
   ```
  
   Since no parameters are specified, the `BLUR` background effect is created.

4. After creating the background effect, use the `cameraStream` object's `addEffect()` method to apply the effect to the camera stream:

   ```js
   const effect = await cameraStream.addEffect(effect);
   ```

5. Enable the effect to observe it in action on the video:

   ```js
   await effect.enable();
   ```

## Apply the Noise Reduction Effect

The noise reduction effect is designed to eliminate background noise from an audio stream, ensuring clear audio during calls. To apply this effect, call the `Meetings` object's `createNoiseReductionEffect()` method with any desired options:

```js
await webex.meetings.createNoiseReductionEffect(options);
```



<table>
  <colgroup>
    <col/>
    <col/>
  </colgroup>
  <tbody>
    <tr>
      <td>
        <strong>Asynchronous</strong>
      </td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>
        <strong>Parameters</strong>
      </td>
      <td>
        options
        
          <table>
            <tbody>
              <tr>
                <th</th>
                <th><strong>Description</strong></th>
                <th><strong>Values</strong></th>
                <th><strong>Required</strong></th>
              </tr>
              <tr>
                <td><code>audioContext</code></td>
                <td>
                   An optional <code>AudioContext</code> for custom behavior. For example:<br/><br/>
                   <code>const audioContext = new AudioContext({sampleRate: 48000});</code>
                </td>
                <td><strong>Object</strong></td>
                <td>No</td>
              </tr>
              <tr>
                <td>mode</td>
                <td>
                  Determines whether to run in <code>WORKLET</code> mode or <code>LEGACY</code> mode for older
                    browsers.
                </td>
                <td>
                  string
                  
                    <table>
                      <tbody>
                        <tr>
                          <td><code>WORKLET</code></td>
                          <td><code>LEGACY</code></td>
                        </tr>
                      </tbody>
                    </table>
                  
                </td>
                <td>
                  Defaults to <code>WORKLET</code>.
                </td>
              </tr>
            </tbody>
          </table>
        
      </td>
    </tr>
    <tr>
      <td colspan="1">
        <strong>Returns</strong>
      </td>
      <td colspan="1">
        A promise that returns the noise reduction effect.
      </td>
    </tr>
  </tbody>
</table>

## Apply the Noise Reduction Effect

To apply the noise reduction effect to a microphone stream:

```js
const microphoneStream = await createMicrophoneStream();

const effect = await webex.meetings.createNoiseReductionEffect();

meetingStreamsLocalAudio.srcObject = microphoneStream.outputStream;

const effect = await microphoneStream.addEffect(effect);

await effect.enable();
```

## Effect Helper Methods

Both effects offer the following helper methods:

- `effect.disable()` - Disables the effect.
- `effect.dispose()` - Removes the effect.
- `effect.setEnabled(true|false)` - Single method to enable or disable the effect. Pass `true` to enable the effect and `false` to disable.
- `stream.getEffectByKind(effectName)` - Return the effect added on the stream (either `noise-reduction-effect` or `virtual-background-effect`).
- `stream.getEffects()` - Retrieve all effects added to the stream.
- `stream.disposeEffects()` - Remove all effects from the stream.
