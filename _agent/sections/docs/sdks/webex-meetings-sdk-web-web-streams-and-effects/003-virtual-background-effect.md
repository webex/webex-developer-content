---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Virtual Background Effect
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects). [Full Markdown](../../../../../docs/sdks/webex-meetings-sdk-web-web-streams-and-effects.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

The Webex Meetings Web SDK version 3.0 introduces new APIs designed to facilitate the management of local media streams for audio, video, and screen sharing. This article explains how the `Streams` object functions with two newly added effects: `VirtualBackgroundEffect` and `NoiseReductionEffect`. Those effects and their corresponding methods are available in the plugin-meetings package.

---



> **Info**
>
> See the [kitchen sink app](https://webex.github.io/webex-js-sdk/samples/browser-plugin-meetings) for examples of the effects.

## Selected section

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
