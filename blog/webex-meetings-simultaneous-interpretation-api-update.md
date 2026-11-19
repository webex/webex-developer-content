---
type: Article
title: Webex Meetings Simultaneous Interpretation API Update
canonical_url: https://developer.webex.com/blog/webex-meetings-simultaneous-interpretation-api-update
content_type: blog
date: '2022-06-09'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-meetings-simultaneous-interpretation-api-update)

To further enable a more inclusive collaboration experience, Webex recently introduced the new Simultaneous Interpretation feature. For meetings and events like legal proceedings, business negotiations, or academic seminars you may need a live interpreter. This feature allows a Webex user to assign live interpreters to unlimited audio channels so that attendees can listen in the language of their choice.

For Scheduling a meeting with this feature, a host can use the same familiar interface in the Webex client or web version. Alternatively, the new Simultaneous Interpretation feature can be scheduled programmatically leveraging the Webex Meetings API. Below we will be going through some of the updated [Webex API changes](https://developer.webex.com/docs/api/changelog) and how to use them to create and update a Webex Meeting.

### Webex Rest API Samples

The Webex Meetings Rest API enables seamless integration of Webex Meetings into your websites and apps. You can schedule meetings, send meeting invitations, list meetings, and more. The full source code for this sample project is available on [Github](https://github.com/WebexSamples/rest-api-samples). You can also find many more samples/examples in the repository that is managed by the Webex Developer Evangelist team [here](https://github.com/WebexSamples).

### Create a Meeting with Simultaneous Interpretation

To Schedule a Meeting, we can make some changes to the create portion of the CRUD Meeting sample code in the Webex REST API Samples repository. We will need to create a variable that we will call `interpreterAry` and use to store the array that will contain the list of Interpreter Objects needed to fulfill the`interpreters` parameter in the `simultaneousInterpretation` object.

```javascript
interpreterAry = [
    {"languageCode1":"en", "languageCode2":"es", "email":"jodoe@example.com", "displayName":"John Doe"},
    {"languageCode1":"es", "languageCode2":"en", "email":"jadoe@example.com", "displayName":"Jane Doe"}
  ];
```

In the above code snippet, the values for keys `languagecode1` and `languagecode2` are strings in standard language format for [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). Interpreters will be translating from `languagecode1` to `languagecode2` for listeners that select this language from the associated channel options. The email value will be the interpreter’s email and a meeting invitation will be sent to this email address upon successful implementation of the API call that will contain this list. See the below code snippet for more details.

```javascript
const body = JSON.stringify({
   title: 'WebDev Meeting w/ Simultaneous Interpretation', 
   start: '2022-08-12T13:51:43-04:00',            
   end: '2022-08-12T14:38:16-04:00',              
   simultaneousInterpretation: {"enabled":true,"interpreters":interpreterAry}
 });
```

The above code is a snippet of the body with required parameters `title`, `start`, and `end`. It includes the optional `simultaneousInterpretation` parameter with its key values `enabled` set to true and `interpreters` set with the array/list of interpreter objects that we previously built. Making these changes to the sample code should produce the same expected output with a status code of 200 and all expected response properties according to the documentation. The same code changes will produce similar results in the update code sample as well.

### Try It Now

A copy of the create sample code is available on GitHub: [https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create](https://github.com/WebexSamples/rest-api-samples/tree/main/meetings/create).

### Engage With Us

The [Webex Developer Community](https://community.cisco.com/t5/webex-for-developers/welcome-to-the-webex-for-developers-forum/m-p/4558386#M321) has dedicated topics, discussion groups, and announcements. Also, follow [Webex Devs](https://twitter.com/webexdevs?lang=en) on Twitter. We encourage you to tell us about your experience using the above sample code.
