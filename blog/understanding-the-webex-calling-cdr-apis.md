---
type: Article
title: Understanding the Webex Calling CDR APIs
canonical_url: https://developer.webex.com/blog/understanding-the-webex-calling-cdr-apis
content_type: blog
date: '2025-12-17'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/understanding-the-webex-calling-cdr-apis)

Until now, there has been only one API that allowed developers to access the raw Call Detail Records (CDRs) from the Webex Calling platform. That API is known, according to the documentation, as the “**Detailed Call History**” API and was accessed with the [/v1/cdr_feed](https://developer.webex.com/calling/docs/api/v1/reports-detailed-call-history/get-detailed-call-history) endpoint.

This month, we have released a new API called the “**Live Stream Detailed Call History**”, which is accessible from the [/v1/cdr_stream](https://developer.webex.com/calling/docs/api/v1/reports-live-stream-detailed-call-history/get-live-stream-detailed-call-history) endpoint. When you view the documentation for this API [here](https://developer.webex.com/calling/docs/api/v1/reports-live-stream-detailed-call-history), it states that Cisco recommends using this new endpoint “as the primary API for customers who need to continuously consume CDRs for custom reporting, analytics applications, or integration into internal data stores.” But what exactly is the difference between the two?

## Let’s take a look at the documentation…
> The `CDR Stream` endpoint will allow customers to call the API as soon as the call ends, typically 1 minute before the current time. It automatically backfills any late records as soon as they are processed in the Webex Calling cloud. These records are then delivered in subsequent API calls, ensuring reliable CDR delivery.
> 
> To retrieve **Detailed Call History** information, you must use a token with the `spark-admin:calling_cdr_read` scope. The authenticating user must have the administrator role "**Webex Calling Detailed Call History API access**" enabled.
> 
> **Detailed Call History** information is available 1 minute after the call ends and the data reaches Webex Calling cloud. Records may be retrieved for up to 12 hours from the time they are stored. For example: if a call's data reaches the Webex Calling cloud at 9:46 AM, the record becomes available from 9:47 AM and remains retrievable until 9:46 PM the same day. Additionally, only 2 hours’ worth of records can be retrieved per request (i.e., 2 hours between the selected start and end times in a single API call).

For those who have used the `/v1/cdr_feed` endpoint, that sounds very similar to the way that endpoint worked, although the 12-hour retention and 2-hour window is new. Viewing the documentation for that endpoint, we see:
> The `CDR Feed` API can query any 12-hour period between 5 minutes ago and 30 days prior to the current UTC time. Only 12 hours of records can be retrieved per request (i.e., the time between the selected start and end times in a single API call). For example: If a call ends at 9:46 AM, the record is available for collection starting at 9:51 AM and remains available until 9:46 AM 30 days later. The maximum query duration starting at 9:51 AM would end at 9:51 PM the same day.

At first glance, that seems like the better endpoint to use. You can pull longer windows of time (12 hours vs. 2 hours) and can get data from as far back as 30 days. So why would Cisco recommend the "**CDR Stream**" instead? Both endpoints need a `startTime` and `endTime` parameter. Both support a `locations` parameter to limit the records to specific Locations, and both allow you to specify a `max` number of records per page between 500 and 5000 records. So, what is the difference?

To answer that, you need to understand the timestamps of the records themselves. A CDR contains a field called "**Start Time**", which indicates when the call represented by the CDR began. There is no field in the CDR itself that indicates when the record was written to the database, so even though you may have a record with a **Start Time** of 11:59, it may not have been written to the CDR database until 12:00, or later if there were any delays in processing the record. When using the `/v1/cdr_feed` endpoint, the `startTime` and `endTime` parameters refer specifically to this "**Start Time**" field within the CDR. The `/v1/cdr_stream` endpoint, on the other hand, uses the `startTime` and `endTime` parameter to refer to **the exact time the record was written to the database**.

### Which CDR API should I use?

Let's think of a real-world example you might encounter. Imagine a script that runs every hour, right at the top of the hour and pulls the CDRs from the previous hour. If a call is placed at 11:59 but lasts 10 minutes, the CDR will not be written to the database until 12:10, one minute after the call ends. The script would have run at 12:00 to retrieve records from 11:00 to 12:00. As you would expect, but probably hadn't thought about before now, that call would not be returned in the response since the record isn't written until ~1 minute after the call ends. But, since the `startTime` and `endTime` parameters refer to the "**Start Time**" field of the CDR itself (which would be 11:59 in this case, because that's when the call started), the script execution at 13:00, which would request calls from 12:00-13:00, would also not return that call. In order to find it using the `cdr_feed` endpoint, you would have to overlap the time windows you are searching for, which could lead to a lot of duplicate entries and wasted processing time, in addition to still leaving a potential gap if a call lasted longer than your query window.

Knowing that the new `cdr_stream` endpoint uses the timestamp when the record was written to the database, it should be clear that this approach is much more reliable. In the previous example, the record would be written to the database at 12:10, so the record will appear in the 12:00-13:00 records, even though the call started during the 11:00-12:00 hour. And even if the record would have been delayed in processing, the record will always be contained in the "new" records the script is requesting, ensuring no records are lost. The documentation refers to automatically backfilling records and this is what it is referring to. You no longer need to manually backfill missing records with subsequent calls to `cdr_feed` with the same time window you used previously.

Now that we understand why this new endpoint is more reliable and why Cisco recommends it to "continuously consume CDRs for custom reporting, analytics applications, or integration into internal data stores", you may be wondering why Cisco didn't simply replace the existing `cdr_feed` logic with this new logic. Why is the old `cdr_feed` still valuable?

To see the value of having both endpoints, let's go back to the example call we have been discussing. If a developer receives a request from their business to create a report that shows "all calls placed or received between 11:00 and 12:00", and that request comes days after the calls have occurred, let's think about what would be returned by each endpoint. As you've seen, using `cdr_stream` with a `startTime=11:00` and `endTime=12:00` would not contain the call from our examples. Instead, using the `cdr_feed` endpoint with the same `startTime` and `endTime` would ensure that all calls placed or received during that window will be returned.

Each endpoint has its own benefit, but the two will likely not be used by the same process. Automated systems that use the `cdr_stream` endpoint will likely insert that data into a data store where the data can be queried directly, eliminating the need for the `cdr_feed` endpoint. Developers who wish to collect reporting data from Webex would benefit from `cdr_feed`.

### Conclusion

As you can see, understanding the differences between these endpoints is essential when deciding which to use for your development needs, but the following advice serves as a good rule of thumb:

*   For continuous processes to pull CDRs from Webex into another data store, use the `cdr_stream` endpoint
*   For historical reporting within 30 days, use the `cdr_feed` endpoint
*   For historical reporting longer than 30 days, or for larger windows of time, the existing `/v1/reports` endpoint should be used. This endpoint has not changed.

<br/>

### Need help? We’ve got you covered…

We are always happy to provide support for these Calling APIs and integrations. If you need help, the [Webex Developer Support Team](https://developer.webex.com/explore/support) is standing by ready to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://community.cisco.com/t5/webex-for-developers/bd-p/disc-webex-developers).
