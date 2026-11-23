---
type: Excerpt
canonical_url: https://developer.webex.com/docs/ea-handling-events-test
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- Creating Event Listeners
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/ea-handling-events-test). [Full Markdown](../../../../docs/ea-handling-events-test.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

---

**[Embedded Apps Guide](https://developer.webex.com/docs/ea-developer-guide-test) > Event Handling**
* * * 

## Selected section

## Creating Event Listeners

The basic pattern for creating event listeners is shown below, where `app` is a `Webex.Application` instance previously created:

```javascript
app.listen().then(function() {
  // listen().then() ok
   app.on(<eventName1>, <callback>);
   app.on(<eventName2>, <callback>);
})
.catch(function (reason) {
  // listen().then() failed
});
```

Or, with JavaScript arrow functions:

```javascript
app.listen().then(() => {
   app.on(<eventName1>, <callback>);
   app.on(<eventName2>, <callback>);
})
.catch(function (reason) {
  // Listen() promise failed
});
```

When the `listen()` promise resolves successfully it indicates that the framework is ready to register your application's callback functions. For example, the following creates listeners for both `meeting.infoChanged` and `application.themeChanged`.

```javascript
app
  .listen()
  .then(() => {
      app.on("meeting.infoChanged", (event) => {
          let meetingId = event.id;
          let conferenceId = event.conferenceId
          // etc..
      })
      app.on("application:themeChanged", (event) => {
        // Call custom function to update theme:
        // updateAppTheme(event);
      })
  })
  .catch(function (reason) {
      console.error("listen: fail reason=" + reason);
  });
```
