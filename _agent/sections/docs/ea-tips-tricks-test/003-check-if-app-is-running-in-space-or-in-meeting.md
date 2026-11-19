---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-tips-tricks-test
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Check if App is Running In-Space or In-Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-tips-tricks-test). [Full Markdown](../../../../docs/ea-tips-tricks-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Workflow**
* * * 

## Selected section

## Check if App is Running In-Space or In-Meeting

In some cases an embedded app may need to determine if it's running in a meeting or a space. One way to do this is to check the value of the [app.displayContext](https://developer.webex.com/docs/embedded-apps-api-reference#Webex.Application+displayContext), which contains one of the following values: `"MEETING_SIDEBAR"`, `"MEETING_STANDALONE_WINDOW"`, `"MEETING_MAINVIEW"`, or `"SPACETAB"`. For example, the following code uses the [includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) function to check if `app.displayContext` contains the string "MEETING". If `includes()` returns `true` the app is running in a meeting, otherwise it's running in a space.

```javascript
    var app = new window.Webex.Application();
    var isMeeting = false;

    app.onReady().then(() => {
        // Check if running in a meeting
        isMeeting = app.displayContext.includes("MEETING");
        if(isMeeting) {
            console.log("I'm running in a meeting");
        } else {
            console.log("I'm running in a space");
        }
    }).catch((errorcode) =>  {
        log("Error: ", Webex.Application.ErrorCodes[errorcode]);
    });
```

<a id="cookies_local_storage"></a>
