---
type: Guide
title: Webex Contact Center Web Widgets | Components | OutdialCall
display_title: OutdialCall
canonical_url: https://developer.webex.com/docs/cc-web-widgets-components-outdialcall
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/cc-web-widgets-components-outdialcall)

The `OutdialCall` component enables agents to make outbound calls directly from the contact center interface.

---

The `OutdialCall` component provides a user interface for agents to initiate outbound calls to customers or other parties. This component is essential for:

- Proactive customer outreach
- Return calls to customers
- Callback campaigns
- Outbound sales or service calls

**Look and feel**:
1. ![1-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7fd1f8ae03bacd40/6972a414f19f6074f5999ec2/1-outdial-call.png?branch=integration&height=400)
2. ![2-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blteea85e80d89ccbdf/6972a41475543f273c3638fd/2-outdial-call.png?branch=integration&height=400)
3. ![3-outdial-call.png](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt4e9f7256328765a0/6972a4140398574b2c825e02/3-outdial-call.png?branch=integration&height=400)

## Import

```js
import { OutdialCall } from '@webex/cc-widgets';
```

## Usage

```js
<OutdialCall />
```

### Error Handling

```js
import { useEffect } from 'react';

useEffect(() => {
  store.setOutdialFailed((reason) => {
    console.log('Outdial call failed: ', reason);
  });

  return () => {
    store.setOutdialFailed(undefined);
  };
}, []);
```

**Note**:

1. Use the `OutdialCall` widget in combination with other required widgets such as `StationLogin`, `UserState`, `TaskList` or `IncomingTask` to see the functionality working end to end.
2. You can use the [Widgets Kitchen Sink](https://widgets.webex.com/samples-cc-react-app/index.html) for reference.

## Features

### Dial Pad

- Visual dial pad for entering phone numbers

### Address Book

The Address Book feature allows agents to access and dial from a centralized contact directory:

- **Contact Directory**: Access to saved contacts and frequently dialed numbers
- **Quick Selection**: Select and dial contacts with a few clicks
- **Contact Search**: Search through the address book to find contacts quickly

### Contact Selection

- Integration with contact lists
- Search and select contacts

## Configuration Notes

- Outbound calls can only be initiated when the agent does not have any other active voice calls
- Outdial permissions must be configured in the contact center system through the [Admin Portal](https://admin.webex.com).
- The `store` must be initialized with a valid access token
- Make sure to wrap the component with `ThemeProvider` and `IconProvider` from Momentum Design
- Address Book contacts must be configured in the contact center system through the [Admin Portal](https://admin.webex.com) for the feature to display available contacts
