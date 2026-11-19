---
type: Article
title: Webex Report Download Using the Webex API
canonical_url: https://developer.webex.com/blog/webex-report-download-using-the-webex-api
content_type: blog
date: '2022-07-18'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/webex-report-download-using-the-webex-api)

One of the first things an enterprise might want to do with the Webex API is to use it to download a report. This is a very typical use case as customers regularly interact with the reports in the GUI of Control Hub. They have found value in downloading the report but want to automate the creation and downloading of the report. In this article, I'll show you how you can create a Python script to accomplish this task.

### Understanding the Report API

In order to successfully download a report, there are some things that you as the developer need to be aware of before you start. Reading this section on the documentation will familiarize yourself with the basic steps needed. Be sure to know that you cannot download a report you created in the GUI. Your developer flow will be that you create your report with the API and you download that report with the API. [This is explained very well in our documentation](https://developer.webex.com/docs/admin#reports-api).

### OAuth and Tokens

Another set of topics that you should know when you get into the Webex API will be OAuth and Tokens. [Check out this blog post to learn more](https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration).

### Create an Integration

[Follow this guide to create an integration](https://developer.webex.com/docs/integrations). Make sure to include the scope `analytics:read_all` so that your integration has the appropriate rights to download a report. Also, be sure to grab two important pieces of information before you leave the integration page, your **Application ID** and your **Application Secret**.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt29b11b2e1dd343d7/62cf1d420c50ad376dfd7cc7/Picture1.png)

### Handling OAuth in Automation

OAuth *feels* like it is meant to require a human each time you run your API, so it would be natural to think that you cannot automate an API call that is protected by an OAuth flow. There is a way that you get to have the best of both worlds. You can have the security of OAuth, but you can leverage the tokens given by the Webex API so that you can still automate the API calls.

The key is knowing which token does what purpose. Let's setup a scenario where you want to create and download a report every month. An **Access token**, which is the token needed to actually get the data from our APIs, expires every 14 days. You might be thinking that every 14 days you'll need to have a person then accept this OAuth flow. But because the **Refresh token** expires every 90 days, and the sole purpose of a Refresh token is to get a new Access token, customers can leverage the Refresh token in our scenario. The Refresh token is what needs to be saved and available to your script as an environment variable. The Access token you get from using your Refresh Token can be saved in memory of the script and discarded in our once-a-month example. If you were doing this more often, you'd rethink this strategy.

### Knowing your template

As this script will be setup to run on a regular interval, the template value will be consistent. You as the developer can choose how you handle this but in my example code I’m showing the user all of the available templates and their associated numbers. If this were production code, you might set the template ID as an environment variable.

### Creating your Report

How will you deal with the changing dates? Again, here is another time that a developer has many choices they could make to solve this problem. Here, since my use case is that this script will run once at the end of each month. I'll simply just get the date of when the script is run and set the start date to the first day of the current month. This will give me my start time and end time for my report to be run.

```python
def _report_creation(self, template: str):
        """ Private function that creates the needed report.
            In this example, the startDate, endDate and siteList
            are hardcoded.
        """
        url = f'{self.base_url}/reports'
        data = {
            "templateId": int(template),
            "startDate": "2022-03-01",
            "endDate": "2022-03-31",
            "siteList": "jhaefner-gasandbox.webex.com"
        }
        response = self.session.post(url=url, json=data)
        if response.status_code != 401:
            json_response = json.loads(response.text)
            log.info(f"Created Report ID: {json_response['items']['Id']}")
            return json_response['items']['Id']
        else:
            log.warning('Access Token was Expired')
```

### Waiting...

Now that you've created your report, Webex is doing all the hard work. You just need to have your script check back in with Webex to see if your report is done yet. Here is where I made a "while loop" to keep checking until the status of the report was "done"

```python
def _check_on_report(self, id: str):
        """ Loop on a 30 second interval checking if the newly created
            report is done and ready to be downloaded.
        """
        url = f'{self.base_url}/reports/{id}'
        report_status = 'not done'
        download_url = ""
        while report_status != 'done':
            response = self.session.get(url=url)
            json_response = json.loads(response.text)
            download_url = json_response['items'][0]['downloadURL']
            report_status = json_response['items'][0]['status']
            print(f"Report status: {json_response['items'][0]['status']}, checking in 30 seconds...")
            time.sleep(30)
        log.info(f'Report Download URL: {download_url}')
        return download_url
 
```

### Download and Cleanup

Once you’ve used the download URL to get your report, you should delete your report from Webex. Not only is it good housekeeping, but you have a limit of how many saved reports you can have. If you exceed that limit, you won't be able to create any more reports.

```python
def _delete_report(self, id: str):
        """ Finally, we need to delete that downloaded report.
        """
        url = f'{self.base_url}/reports/{id}'
        response = self.session.delete(url=url)
        if response.status_code == 204:
            log.info(f'Deleted Report ID: {id}')
            return response.status_code
        else:
            log.error(f'Deleted Report ID: {id}, status code: {response.status_code}')
            return response.status_code
 
```

### Conclusion

Leveraging the Webex API to create and download Reports can be setup in such a way that an enterprise can automate this flow. To see this example code, please visit [https://github.com/justinhaef/py_webex_report_downloader](https://github.com/justinhaef/py_webex_report_downloader) and follow the Github read me to try it out. I also walk through this code in a very short video here: [https://app.vidcast.io/share/87f61a88-6073-40b3-9f5c-7760ea7d6f63](https://app.vidcast.io/share/87f61a88-6073-40b3-9f5c-7760ea7d6f63).
