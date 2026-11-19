---
type: Excerpt
canonical_url: https://developer.webex.com/docs/meetings
lane: production
source_revision: cms-sha256:eef02d9689815c50a76fcf18add9b322a54bd5fd836885db6fc040057975c564
publication_state: verified_published_snapshot
heading_hierarchy:
- Restrictions on Updating a Meeting
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/meetings). [Full Markdown](../../../../docs/meetings.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

Setup and context to read: [Meetings API Scopes](003-meetings-api-scopes.md) [User Level Authentication and Scopes](004-user-level-authentication-and-scopes.md) [Admin/Organization Level Authentication and Scopes](005-admin-organization-level-authentication-and-scopes.md) [Group Level Authentication and Scopes](006-group-level-authentication-and-scopes.md) [Compliance Officer Level Authentication and Scopes](007-compliance-officer-level-authentication-and-scopes.md) [Scopes and User Roles](008-scopes-and-user-roles.md) [Warnings](014-warnings.md)

## Article introduction

The new Webex Meetings REST API enables seamless integration of Webex Meetings into your websites, apps, and services. Schedule meetings, invite meeting attendees, update preferences, and more.

---



> **Warning**
>
> **XML API Deprecation Announcement**  
> The Meetings-related XML APIs will be deprecated and the End-of-Support (EoS) date is planned for the second half of 2023. Cisco will continue to resolve bugs up to this date, but new features will only be implemented for the REST APIs suite. The End-of-life (EoL) timeframe for Meetings-related XML APIs is targeted for **March 31, 2024**, at which time the APIs will be retired. For more information on how to migrate from XML to REST APIs, please see the [Webex Meetings XML to REST Migration Guide](https://developer.cisco.com/docs/webex-meetings/#xml-to-rest-migration-guide). User management APIs such as `CreateUser`, `SetUser`, `DelUser`, etc. are **NOT** affected by this EOL announcement.

## Selected section

## Restrictions on Updating a Meeting

When updating a meeting, there are different restrictions for different meeting types. It's important for a developer to understand these restrictions to avoid confusion and handle any restriction-related errors when they occur.

There are some general rules for updating a meeting. They are listed below.

### Rule 1. `start` and `end` cannot be a time before the current time

This rule applies to meeting series and scheduled meeting.

When updating a meeting series or a scheduled meeting, the `start` and `end` in specified `timezone` cannot be a time before the current time. For example, assume that the current time is `2021-05-28T14:00:00+08:00`, if update a meeting series, or a scheduled meeting with `start` of `2021-05-27T14:00:00+08:00` and `timezone` of `Asia/Shanghai`, it will fail saying that "Parameter 'start' or 'end' is before current time". Please note that the default `timezone` is `UTC` if not specified explicitly.

### Rule 2. Limit for duration between `start` and `end`

This rule applies to meeting series and scheduled meeting.

Duration between `start` and `end` cannot be shorter than 10 minutes or longer than 24 hours.

### Rule 3. Update is forbidden when an associated meeting instance is in progress

This rule applies to meeting series and scheduled meeting.

When a meeting instance is in-progress, its parent scheduled meeting and grandparent meeting series cannot be updated. In fact, when a meeting instance is in-progress, the state of the parent scheduled meeting is `ready` which means that currently this scheduled meeting is ready to join, and the state of the grandparent meeting series is `inProgress` which means that a meeting instance of the series is currently happening. Neither the parent scheduled meeting, nor the grandparent meeting series can be updated until the ongoing meeting instance is ended. If break this rule, it'll fail saying that "Meeting is in progress".

### Rule 4. Update is forbidden for a meeting instance

This rule applies to meeting instance.

It's totally forbidden to update any meeting instance of any state. It fails with an error message like "Meeting ID '06263e1088604fc1b3ca17fbe49fe97d_I_195989045032040979' is not allowed for this API."

### Rule 5. Update is forbidden to cross recurring interval

This rule applies to scheduled meeting.

#### What is a recurring interval

When a meeting series has been scheduled, each scheduled meeting of this meeting series has its own "territory of time". It means that any other scheduled meeting of the same meeting series cannot be updated to fall into the range of time of this scheduled meeting. Specifically, each scheduled meeting has its original `timezone` when the parent meeting series was scheduled. It can be an explicitly specified value such as `Asia/Shanghai` or `UTC` by default if not specified explicitly. Generally, the recurring interval of a scheduled meeting begins at `00:00:00` (inclusive) in the original timezone of the day of `start`, and ends at `00:00:00` (exclusive) in the original timezone of the day of the next scheduled meeting of the same meeting series. However, there's exception for the first and the last scheduled meeting of a meeting series. The first one has no beginning, and the last one has no end. It's explained in detail below with examples of daily meetings and weekly meetings. The rule for other meetings, e.g. yearly meetings, is similar.

##### 1. Recurring intervals of a daily meeting series

<img src="https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6bc10925764a4209/60c00566324cea0e69782c3f/Restrictions_On_Updating_A_Meeting-01._Daily.jpg" width="1000">

**Fig. 1** Recurring intervals of a daily meeting series

Fig. 1 illustrates the recurring intervals of a daily meeting series with four scheduled meetings.

* **Recurring interval of `d1`:** No beginning, to `2021-04-20T00:00:00+08:00` (exclusive).
* **Recurring interval of `d2`:** From `2021-04-20T00:00:00+08:00` (inclusive) to `2021-04-21T00:00:00+08:00` (exclusive).
* **Recurring interval of `d3`:** From `2021-04-21T00:00:00+08:00` (inclusive) to `2021-04-22T00:00:00+08:00` (exclusive).
* **Recurring interval of `d4`:** From `2021-04-22T00:00:00+08:00` (inclusive), no end.

##### 2. Recurring intervals of a weekly meeting series

![Restrictions On Updating A Meeting - Weekly](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltebb5e4e912c7ae25/60c005671b32a31d5305bd14/Restrictions_On_Updating_A_Meeting-02._Weekly.jpg)

**Fig. 2** Recurring intervals of a weekly meeting series

Fig. 2 illustrates the recurring intervals of a weekly meeting series with four scheduled meetings. Please note that recurring intervals of a weekly meeting can be of different lengths, and a single recurring interval may cross days.

* **Recurring interval of `w1`:** No beginning, to `2021-06-04T00:00:00+08:00` (exclusive).
* **Recurring interval of `w2`:** From `2021-06-04T00:00:00+08:00` (inclusive) to `2021-06-08T00:00:00+08:00` (exclusive).
* **Recurring interval of `w3`:** From `2021-06-08T00:00:00+08:00` (inclusive) to `2021-06-11T10:00:00+08:00` (exclusive).
* **Recurring interval of `w4`:** From `2021-06-11T10:00:00+08:00` (inclusive), no end.

##### 3. Recurring intervals of the first and last scheduled meetings of a meeting series

![Restrictions On Updating A Meeting - The First and The Last](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7e5fb43b46dd8ab1/60c00568d475801b9d54f8e7/Restrictions_On_Updating_A_Meeting-03._The_first_and_the_last.jpg)

**Fig. 3** Recurring intervals of the first and last scheduled meetings of a meeting series

Please pay attention to the recurring intervals of the first and the last scheduled meetings of a meeting series:

* The recurring interval of the first scheduled meeting of a meeting series has no beginning. For instance, Fig. 3 illustrates recurring intervals of a daily meeting series with three scheduled meetings. The recurring interval of `d1` which is highlighted in green has no beginning and ends at `2021-04-20T00:00:00+08:00` (exclusive). Therefore, `d1` can be updated to `d1-01` or `d1-02`.
* The recurring interval of the last scheduled meeting of a meeting series has no end. For instance, in Fig. 3, the recurring interval of `d3` which is highlighted in blue begins at `2021-04-21T00:00:00+08:00` and has no end. Therefore, `d3` can be updated to `d3-01` or `d3-02`.

#### Cross-recurring-interval update is forbidden

Based on the `recurring interval` concept, cross-recurring-interval update is forbidden. If break this rule, it'll fail with an error message like "meeting.err.two_meeting_schedule_at_same_day". Specifically, meetings RESTful API examines `start` against crossing-recurring-interval behavior when updating a scheduled meeting, but it doesn't examine `end` against this rule.

##### 1. Update scheduled meetings of a daily meeting series successfully

![Restrictions On Updating A Meeting - Update Daily Success](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt6419d17597fdaa5c/60c005682d95121b9b3d15c5/Restrictions_On_Updating_A_Meeting-04._Update_Daily_Success.jpg)

**Fig. 4** Update scheduled meetings of a daily meeting series successfully

Fig. 4 illustrates non-cross-recurring-interval updates for scheduled meetings of a daily meeting series. All the updates in Fig. 4 are within the same recurring interval and succeed. For example:

* **`d1` to `d1-s1`:** This update is within `d1`'s recurring interval. It makes the previously `missed` `d1` to be `ready` again.
* **`d2` to `d2-s1`:** This update is within `d2`'s recurring interval. It makes `d2` a little earlier in the same day.
* **`d2` to `d2-s2`:** This update is within `d2`'s recurring interval. It makes `d2` a little later in the same day.
* **`d4` to `d4-s1`:** This update is within `d4`'s recurring interval. It makes `d4` a little earlier in the same day.
* **`d4` to `d4-s2`:** This update is within `d4`'s recurring interval. It makes `d4` a little later in the same day.
* **`d4` to `d4-s2`:** This update is within `d4`'s recurring interval. It makes `d4` a little later in the same day.
* **`d4` to `d4-s3` or `d4-s4`:** This update is within `d4`'s recurring interval. It moves `d4` to the next day or even later. However, they are both within the recurring interval of `d4` since `d4` is the last scheduled meeting of the parent meeting series. It doesn't break `rule 5`.

##### 2. Update scheduled meetings of a daily meeting series crossing recurring interval

![Restrictions On Updating A Meeting - Update Daily Failure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt03b31b621372bc65/60c0056885c4c2118e316fa5/Restrictions_On_Updating_A_Meeting-05._Update_Daily_Failure.jpg)

**Fig. 5** Update scheduled meetings of a daily meeting series crossing recurring interval

Fig. 5 illustrates cross-recurring-interval updates for scheduled meetings of a daily meeting series. All the updates in Fig. 5 break `rule 5` and fail. For example:

* **`d1` to `d1-f1`:** This update moves `d1` to a time before the current time and breaks `rule 1`.
* **`d2` to `d2-f1`:** This update moves `d2` to the previous day and breaks `rule 5`.
* **`d2` to `d2-f2`:** This update moves `d2` to the next day and breaks `rule 5`.
* **`d3` to `d3-f4`:** This update moves `d3` to two days later and breaks `rule 5`.
* **`d4` to `d4-f2`:** This update moves `d4` to two days ago and breaks `rule 5`.

##### 3. Update scheduled meetings of a weekly meeting series successfully

![Restrictions On Updating A Meeting - Update Weekly Success](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt00749dbe2c63e863/60c00569fbd63412d4133e4f/Restrictions_On_Updating_A_Meeting-06._Update_Weekly_Success.jpg)

**Fig. 6** Update scheduled meetings of a weekly meeting series successfully

Fig. 6 illustrates non-cross-recurring-interval updates for scheduled meetings of a weekly meeting series. All the updates in Fig. 6 are within the same recurring interval and succeed. For example:

* **`w1` to `w1-s1`:** This update is within `w1`'s recurring interval. It moves the previously `missed` `w1` to the next day and makes it `ready` again. It crosses day, but it doesn't cross recurring interval. So, it doesn't break `rule 5`.
* **`w1` to `w1-s2`:** This update is within `w1`'s recurring interval. It moves the previously `missed` `w1` to two days later and makes it `ready` again. It crosses day, but it doesn't cross recurring interval. So, it doesn't break `rule 5`.
* **`w2` to `w2-s1`:** This update is within `w2`'s recurring interval. It moves `w2` a little earlier in the same day.
* **`w2` to `w2-s3`:** This update is within `w2`'s recurring interval. It moves `w2` three days later. It crosses day, but it doesn't cross recurring interval. So, it doesn't break `rule 5`.
* **`w4` to `w4-s2`:** This update is within `w4`'s recurring interval. It moves `w4` to the two days later or even later than that. However, it's within `w4`'s recurring interval since `w4` is the last scheduled meeting of the parent meeting series. It doesn't break `rule 5`.

##### 4. Update scheduled meetings of a weekly meeting series crossing recurring interval

![Restrictions On Updating A Meeting - Update Weekly Failure](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltea6b9452560304eb/60c0056a68689d78c86312bc/Restrictions_On_Updating_A_Meeting-07._Update_Weekly_Failure.jpg)

**Fig. 7** Update scheduled meetings of a weekly meeting series crossing recurring interval

Fig. 7 illustrates cross-recurring-interval updates for scheduled meetings of a weekly meeting series. All the updates in Fig. 7 break `rule 5` and fail. For example:

* **`w1` to `w1-f1`:** This update moves `w1` to a time before the current time and breaks `rule 1`.
* **`w1` to `w1-f2`:** This update moves `w1` to the next recurring interval and breaks `rule 5`.
* **`w2` to `w2-f1`:** This update moves `w2` to the previous recurring interval and breaks `rule 5`.
* **`w2` to `w2-f2`:** This update moves `w2` to the next recurring interval and breaks `rule 5`.
* **`w2` to `w2-f3`:** This update moves `w2` to the last recurring interval and breaks `rule 5`.
* **`w4` to `w4-f2`:** This update moves `w4` to the second recurring interval and breaks `rule 5`.

##### 5. Boundary cases

![Restrictions On Updating A Meeting - Boundary Cases](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blta64e15576e40e2c5/60c0056bf8aee612d399694a/Restrictions_On_Updating_A_Meeting-08._Boundary_Cases.jpg)

**Fig. 8** Boundary cases

Meetings RESTful API examines `start` against crossing-recurring-interval behavior when updating a scheduled meeting, but it doesn't examine `end` against this rule. In other words, if the target `start` crosses recurring interval, the update breaks `rule 5`; if the target `start` doesn't cross recurring interval, it doesn't break `rule 5`.

Fig. 8 illustrates various boundary cases of updating a scheduled meeting of a daily meeting series. The upper part is moving `d1` towards `d2` and the lower part is moving `d2` towards `d1`.

The upper part is forward boundary cases:

* **`d1` to `d1-b1`:** This update doesn't cross recurring interval. It doesn't break `rule 5`.
* **`d1` to `d1-b2`:** The target `end` is on the boundary but the target `start` doesn't cross boundary. It doesn't break `rule 5`.
* **`d1` to `d1-b3`:** The target `end` is in the next recurring interval but the target `start` doesn't cross boundary. It doesn't break `rule 5`.
* **`d1` to `d1-b4`:** The target `start` is on the boundary and the target `end` is in the next recurring interval. Since a recurring interval is left-inclusive and right-exclusive, it breaks `rule 5`.
* **`d1` to `d1-b5`:** Both the target `start` and `end` are in the next recurring interval. It breaks `rule 5`.

The lower part is backward boundary cases:

* **`d2` to `d2-b1`:** This update doesn't cross recurring interval. It doesn't break `rule 5`.
* **`d2` to `d2-b2`:** The target `start` is on the boundary. Since a recurring interval is left-inclusive and right-exclusive, it doesn't break `rule 5`.
* **`d2` to `d2-b3`:** The target `start` is in the previous recurring interval. It breaks `rule 5`.
* **`d2` to `d2-b4`:** The target `start` is in the previous recurring interval and the target `end` is on the boundary. It breaks `rule 5`.
* **`d2` to `d2-b5`:** Both the target `start` and `end` are in the previous recurring interval. It breaks `rule 5`.

![Restrictions On Updating A Meeting - Cross-Day Cases](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf2234ea604715cd4/60c0056c68689d78c86312c0/Restrictions_On_Updating_A_Meeting-09._Cross-Day_Cases.jpg)

**Fig. 9** Cross-day cases

There're extreme situations where the parent meeting series was scheduled crossing-day. Fig.9 illustrates a daily meeting series of which the `start` is in some day while the `end` is in the next day. `d2`, `d3` and `d4` are successive scheduled meetings of the series. Here're the recurring intervals of `d3` and `d4`:

* **Recurring interval of `d3`:** From `2021-04-20T00:00:00+08:00` (inclusive) to `2021-04-21T00:00:00+08:00` (exclusive).
* **Recurring interval of `d4`:** From `2021-04-21T00:00:00+08:00` (inclusive) to `2021-04-22T00:00:00+08:00` (exclusive).

The following updates break `rule 5`:

* **`d3` to `d3-01`:** The target `start` is in the previous recurring interval. It breaks `rule 5`.
* **`d3` to `d3-02`:** Same as above.
* **`d3` to `d3-03`:** Same as above.
* **`d3` to `d3-10`:** The target `start` is in the next recurring interval. It breaks `rule 5`.
* **`d3` to `d3-11`:** Same as above.

### Restrictions table

To summarize, the restrictions on updating a meeting of different types are listed in the table below:



| Meeting type | Restrictions on updating meeting of this type |
|---|---|
| Meeting series | Rule 1, 2, 3 |
| Scheduled meeting | Rule 1, 2, 3, 5 |
| Meeting | Rule 4 |
