---
type: Article
title: Webex Detailed Call History API
canonical_url: https://developer.webex.com/blog/webex-detailed-call-history-api
content_type: blog
date: '2023-01-23'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-detailed-call-history-api)

Webex Calling customers have long been able to download their historical call detail records from the Control Hub. They have also been able to create and download these reports using the API. What some customers have been waiting for is a quicker way to get the call details in a programmatic way. In December 2022, Cisco release a new API just for this use case. This API provides access to calls that have completed **between 48 hours ago to 5 minutes ago**.

### Understanding the Detailed Call History API

Users do have some up font work to access this API. First, you’ll notice that this has a different API endpoint, other Webex APIs go to [https://webexapis.com/v1](https://webexapis.com/v1). To use this new API, you’ll need to point your code to [https://analytics.webexapis.com/v1](https://analytics.webexapis.com/v1). This does not change how you will authenticate to Webex to get your Access Token and Refresh Token, that still stays the same. Follow [this guide](https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration) for any questions on how to setup your authentication. For my demo code, I have the Redirect URL going to `https://localhost:8080/webex-teams-auth.html`.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf0428acdec07931d/63c9a475184b72418acdd1d1/webex-detailed-call-history-1.png)

Next, adding a specific scope (`spark-admin:calling_cdr_read` and `spark-admin:locations_read`) in your code as well as your [integration](https://developer.webex.com/docs/integrations) isn’t anything new for Webex APIs but what is new is making sure that your user who creates the integration has a specific role set in Control Hub allowing access to this API.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt9249645ff4fbc1f7/63c9a475be10fd14ecb46293/webex-detailed-call-history-2.png)

Once you have your scopes, Control Hub rights and new API endpoint you’re good to start querying this API. I’ve created some example code that we can step through to help understand the basics of this API. Hopefully after this article you’ll be able to take these basic concepts and create some business value for your organization.

### Code Overview

For this demonstration, I decided to create a Command Line Interface application. IT administrators have used CLI applications for a variety of different use cases. For this demo, we have 3 things we need to solve in the CLI: Authentication, Locations and Analytics. The authentication is the OAuth2.0 flow that we’ve come to understand. Once the user has setup the Integration and copied the Client ID and Secret ID into the .env file, the CLI application is ready to be used. Kicking off the `python webex auth refresh` will start the OAuth2.0 process, the user will need to authenticate to Webex and agree to the scopes being requested by the integration. This CLI application will then save the Access Token and Refresh Token into the same .env file to be used by the other aspects of this CLI application.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltecd6d419102150f0/63c9a4765d5a091065ee1021/webex-detailed-call-history-3.png)

Once we’re authenticated and we have our Access and Refresh Tokens in our .env file, we can move on to doing some API calls. In this demo application we’re going to request only the call detail history for a specific site, so first we need to list out our location names. Note that the Detailed Call History doesn’t require a site be listed for the API query but for my demo I’m using it to show how it can be leveraged to reduce the data returned by the API. By typing `python webex location list` we will get a list of names of all our locations. The user will then use this list later to specify which location they want the call records for.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltddbd37623248b10d/63c9a476e97936109ef2c0b3/webex-detailed-call-history-4.png)

Now we’re ready to query the new API for the call history for a location. By typing `python webex analytics generate (site name)` we’ll be greeted with a series of questions asking to specify the date and time of our query. We need to enter in our start and end times, remembering that we cannot request records older then 48 hours and younger then 5 minutes for the time of query. Also please be advised that all times are in UTC.

```python
def create_report(self, start: str, end: str, site: str):
 payload = {
   'startTime': start,
    'endTime': end,
    'locations': site,
   # 'max': 
  }
  # this is finally where we make our API call for Analytics
  response = self.session.get(url=self.base_url, params=payload)
  return response.text
```

Finally, we’ll get back the results of our query in JSON format. Organizations could modify the code at this point to save off the data to another system for a deeper investigation.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltd6f05045150f5371/63c9a4761b4d922d042bc9bb/webex-detailed-call-history-5.png)

### Conclusion

The code that was used is all [publicly available here](https://github.com/justinhaef/WxCalling_CDR) but most of the code is to just make the CLI application user friendly. Making the API requests can be accomplished many ways, this demo just shows one way of doing it.
