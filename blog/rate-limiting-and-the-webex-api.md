---
type: Article
title: Rate Limiting and the Webex API
canonical_url: https://developer.webex.com/blog/rate-limiting-and-the-webex-api
content_type: blog
date: '2025-04-14'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/rate-limiting-and-the-webex-api)

> **Info**
>
> This blog has been updated for 2025.



In this blog, we’ll provide a guide to implementing rate limiting with the Webex API to gracefully allocate resources across the shared Webex customer base, preventing excessive request errors in your own app, and ensure efficient API call management. We’ll examine practical solutions like using the `Retry-After` header to handle HTTP 429 errors and offers a Python code example for seamless integration in your own environment.

To protect the Webex environment, especially from distributed denial of service attacks, the API has rate limits in place for the different resources available for use, such as `/messages` and `/rooms`. These limits will vary depending on the calls being made, how resource intensive that call is on the servers, and how many servers are actively in routing – and is subject to change as needed to protect all use cases from failing in the event of a large batch of requests.

### A Rate Limiting Solution

So, what should be done if you want to make API calls very frequently, but don’t want to hit errors and lose requests by going over the rate limit?  The answer is to use the `Retry-After` Header that is returned with an `HTTP 429` error.  The `Retry-After` header defines the number of seconds you’ll need to wait before sending API requests again.

### Implementing Rate Limiting in Python

The Python app that follows pulls the list of rooms available to the user (using a single user or bot’s bearer token), as fast as possible.  Normally, it would be recommended to put wait time between continuous looping requests, to avoid hitting the rate limit entirely.  However, since that rate limit might be reached anyway depending on the resource availability, it’s important to handle the likely possibility you’ll catch a 429 here and there.

Basically, we make a call to the integrations URL continuously and look for an error in each response.  If the error is a status code 429, we check the wait time relayed to us in the `Retry-After` header and sleep for the time specified before starting again.  If there’s an error, but it isn’t a `429`, we break out of the loop because something else is wrong.  Maybe you had a bad bearer token, or maybe there is a general error with the format of the request.



> **Info**
>
> Since this code can run forever if implemented properly, you’ll need to Ctrl+C to kill it in the Terminal itself – make sure you don’t let it go on indefinitely or you could be flagged depending on how many requests are made and for how long.



### The Python Application

The initial portion of the application is making the call to the rooms resource to get the rooms over and over, whereas the latter section beginning with the line:

```python
except urllib.error.HTTPError as e:
```

defines what to do if a `429` error is encountered – print out the content of the error and then extract the value of the Retry-After header for use in the sleep. Here’s the full app (it’s short so we’ll provide the whole thing):

```python
import urllib.request
import urllib.error
import json
import time

def sendWebexGET(url):
    request = urllib.request.Request(url,
                                     headers={"Accept": "application/json",
                                              "Content-Type": "application/json"})
    request.add_header("Authorization", "Bearer " + bearer)
    response = urllib.request.urlopen(request)
    return response

bearer = "PERSONAL_ACCESS_TOKEN_HERE"

while True:
    try:
        result = sendWebexGET('https://webexapis.com/v1/rooms')
        print(result.getcode(), time.time(), result.headers['trackingId'])
        except urllib.error.HTTPError as e:
        if e.code == 429:
            print('code', e.code)
            print('headers', e.headers)
            print('Sleeping for', e.headers['Retry-After'], 'seconds')
            sleep_time = int(e.headers['Retry-After'])
            while sleep_time > 10:
                time.sleep(10)
                sleep_time -= 10
                print('Asleep for', sleep_time, 'more seconds')
            time.sleep(sleep_time)
        else:
            print(e, e.code)
            break
```

It’s important to note that it’s possible to send a request after receiving a 429 without getting an error; there are many servers involved with handling a request, so just because you’ve hit the rate limit of one, does not mean you’ve hit the rate limit of all.  However, you’re probably pretty close to failing on every server, so it’s best to wait for the time described by `Retry-After` upon detecting the very first `429`.

### Run the Application

To run the application, save the code in a filename with the extension .py, replace `PERSONAL_ACCESS_TOKEN_HERE `with your personal access token from the Webex developer portal and enter:

`python <your-filename.py>`

You should see output along the lines of:

```bash
$ python foobar.py
200 1743697618.5233638 ROUTERGW_1862482a-c1b9-4c73-bc6b-ffea30a609a7
200 1743697619.5045638 ROUTERGW_f2395a15-1b0d-4f01-9020-7a42fb480f8c
200 1743697620.6093526 ROUTERGW_e4fcb023-ba3a-40e3-b383-9a5ac31188cd
200 1743697621.1333084 ROUTERGW_cbdb5f0c-a9ba-4351-84a7-833a7a43e3db
200 1743697621.6740065 ROUTERGW_26fd34d4-0205-426a-88f1-68183d5cde80
200 1743697622.1625683 ROUTERGW_a4251c0d-b7a9-45e5-9c45-d8befc16157f
200 1743697622.6426196 ROUTERGW_b077d943-e515-41ba-81ba-d64df820aee3
```

Terminate the script when you’re ready with `Ctrl-C`.

The full code can be found on our [Github](https://github.com/WebexSamples/WebexRetryAfterDemo).

### In Closing

As always, if you have any questions, please contact devsupport@webex.com 24/7/365 - we’re happy to help!
