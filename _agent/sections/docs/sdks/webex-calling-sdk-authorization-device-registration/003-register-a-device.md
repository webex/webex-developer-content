---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Register a Device
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/webex-calling-sdk-authorization-device-registration). [Full Markdown](../../../../../docs/sdks/webex-calling-sdk-authorization-device-registration.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

Authorization and device creation are crucial initial steps in leveraging the full capabilities of the calling SDK. Authorization ensures secure access and permissions for developers, while device creation establishes the necessary endpoint for enabling voice and video communication features in your application.

## Selected section

## Register a Device

The line object can be used to perform various line operations including device registration. The device registration process can be begun by using the `line` object's `register()' method:

```js
line.register();
```



| **Asynchronous** | No |
| --- | --- |
| **Parameters** | No parameters required |
| **Returns** | undefined |



> **Info**
>
> The `register()` method only begins the registration process. It does not mean the registration is complete.



### Determine if Registration is Successful

The `register` method only begins the registration process. To verify that the device registration is successful, register a callback to listen for the `registered` event:

```js
line.on('registered', (line: ILine) => {
    // Store the line registration details
}
```

With the help of the `registered` event, you'll know the both that the registration has completed sucessfully and also have access to the `line` detials. 



> **Info**
>
> The event subscription must happen before making the `register()` call.
