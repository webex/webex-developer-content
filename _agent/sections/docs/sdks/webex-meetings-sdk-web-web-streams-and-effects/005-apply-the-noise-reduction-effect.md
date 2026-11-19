---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-meetings-sdk-web-web-streams-and-effects
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Apply the Noise Reduction Effect
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
