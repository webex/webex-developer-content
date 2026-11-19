---
type: Guide
title: Webex Contact Center Web Widgets | Components | StationLogin
display_title: StationLogin
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-stationlogin
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-stationlogin)

The `StationLogin` component allows agents to perform station login and select the type of channel they want to use for establishing voice connections.

---

The `StationLogin` component provides a user interface for agents to log in to their contact center station and choose from different connection types:

- **Desktop**: Uses WebRTC for voice communication
- **Extension**: Allows using a softphone or a hardphone extension
- **Dial Number**: Allows using a PSTN phone number

**Look and feel**:

When profile mode is not enabled

 1. ![1-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1d5c701c7da5b6e1/6972a49190363d5380c29719/1-station-login.png?branch=integration&width=560)
 2. ![2-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt1450dc2fb97d08f5/6972a49133e29d9740396545/2-station-login.png?branch=integration&width=560)
 3. ![3-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blte0a2c877cfa2cff9/6972a491821629a776931257/3-station-login.png?branch=integration&width=560)
 4. ![4-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt739a744b7aacbe4d/6972a49190363d3327c29715/4-station-login.png?branch=integration&width=560)

When profile mode is enabled

![5-station-login.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6317c86469143512/6972a491f19f60601b999ec6/5-station-login-profile-mode.png?branch=integration&width=560)

**Note**: When profile mode is enabled, you can change your StationLogin mode.

## Import

```js
import { StationLogin } from '@webex/cc-widgets';
```

## Props

| Prop              | Type                            | Required | Description                                                                                               |
| ----------------- | ------------------------------- | -------- | --------------------------------------------------------------------------------------------------------- |
| `onLogin`         | `() => void`                    | No       | Callback function triggered when login is successful                                                      |
| `onLogout`        | `() => void`                    | No       | Callback function triggered when logout occurs                                                            |
| `onCCSignOut`     | `() => void`                    | No       | Callback function triggered when contact center sign out occurs                                           |
| `onSaveStart`     | `() => void`                    | No       | Callback function triggered when save starts. This is for the `profileMode`                               |
| `onSaveEnd`       | `(isComplete: boolean) => void` | No       | Callback function triggered when save ends. This is for the `profileMode`                                 |
| `profileMode`     | `boolean`                       | No       | Enable or disable profile mode. Default: `false`                                                          |
| `doStationLogout` | `boolean`                       | No       | Whether to perform station logout when the Signout button is clicked after station login. Default: `true` |

## Usage Example

### Profile Mode Enabled

```js
<StationLogin profileMode={true} onSaveStart={handleSaveStart} onSaveEnd={handleSaveEnd} />
```

### Profile Mode Disabled

```js
<StationLogin
  profileMode={false}
  onLogin={onLogin}
  onLogout={onLogout}
  onCCSignOut={onCCSignOut}
  doStationLogout={true}
/>
```

Callback

```js
const onLogin = () => {
  console.log('Login successful');
};

const onLogout = () => {
  console.log('Logged out');
};

const onCCSignOut = () => {
  console.log('CC Sign Out triggered');
};

const handleSaveStart = () => {
  console.log('Save start called');
};

const handleSaveEnd = (isComplete: boolean) => {
  console.log('Save end called: ', isComplete);
};
```

## Configuration Notes

- The `allowMultiLogin` option in the webex config works specifically for station login types "Extension" and "Dial Number". Please check the [Quickstart Guide](https://developer.webex.com/docs/cc-web-widgets-quickstart) for the config.
- The component requires proper initialization of the `store` before rendering
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design
