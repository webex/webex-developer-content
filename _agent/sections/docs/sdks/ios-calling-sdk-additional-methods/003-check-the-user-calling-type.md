---
type: Excerpt
canonical_url: https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Check the User Calling Type
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/sdks/ios-calling-sdk-additional-methods). [Full Markdown](../../../../../docs/sdks/ios-calling-sdk-additional-methods.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This article describes additional methods available in the Webex Calling iOS SDK.

---



> **Info**
>
> The Mobile SDK supports a maximum of two concurrent incoming calls. A third incoming call is automatically ignored or silently dismissed. Only one call can be in a resumed state at any time.

## Selected section

## Check the User Calling Type

The SDK supports various calling types, such as CUCM and WebexCalling. A user is associated with one calling type at most. Use `webex.phone.getCallingType()` method to check the user's calling type:

```swift
if(webex.phone.getCallingType() == Phone.CallingType.WebexCalling){
    // Indicates Webex Calling is supported for the signed-in user.
}
```
