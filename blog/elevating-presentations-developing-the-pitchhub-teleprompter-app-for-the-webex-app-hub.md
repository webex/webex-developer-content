---
type: Article
title: 'Elevating Presentations: Developing the PitchHub Teleprompter App for the Webex App Hub'
canonical_url: https://developer.webex.com/blog/elevating-presentations-developing-the-pitchhub-teleprompter-app-for-the-webex-app-hub
content_type: blog
date: '2023-09-29'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/elevating-presentations-developing-the-pitchhub-teleprompter-app-for-the-webex-app-hub)

Hey Cisco Developers, allow me to introduce myself – I'm Cary Bran the Chief Product Officer at PitchHub, a startup on a mission to redefine how everyone can deliver amazing presentations. Having walked the halls of Cisco as an engineer and technical leader a past life, I have seen first-hand the innovation and passion Cisco has had for developers. Today, I'm thrilled to share some insights on our development journey in bringing our productivity solution, the PitchHub Teleprompter App, to the Webex App Hub ([https://apphub.webex.com/applications/pitchhub-teleprompter-pitchhub](https://apphub.webex.com/applications/pitchhub-teleprompter-pitchhub)).

### PitchHub: Transforming Presentation Dynamics

At PitchHub ([https://www.pitchhub.com](https://www.pitchhub.com/)), we're passionate about enhancing presentation experiences. Founded in 2019, we have built a full suite of tools making it easy for video content creators to deliver amazing videos. In the wake of the pandemic, we were all remote and really needed to be our best while presenting ourselves over video. PitchHub identified a job to be done for the millions of users out there trying to deliver great presentations within an in-meeting or in-webinar construct.

Presenting is a teachable skill and no matter how competent the speaker is, everyone can benefit from a little in-meeting confidence boost when it comes to delivering their best presentation possible. Our mission has been to help users do just that; be amazing presenters. As a first step, we decided to tackle bringing an integrated teleprompter experience to the WebEx client as an embedded application. The PitchHub Teleprompter app aims to boost the presenter’s confidence, fluidity, and engagement. To bridge the gap between our vision and reality required a partnership between our small, but mighty, team and the Webex Developer team.

### Leveraging Webex Embedded App SDK

The PitchHub Teleprompter app is built on React JS and is hosted on AWS. To maintain a high level of code reuse and to deliver the teleprompter experience inside the context of a Webex meeting we selected the Webex Embedded App approach for our app. The logical choice for us was to use the JavaScript Webex Embedded App SDK. Integration into the React app was simple, and our engineering team had zero issues with the Webex JavaScript SDK.

### Setting up the Webex Sandbox

PitchHub is a small startup and as is true with most startups, we are very budget constrained. I have worked at many large companies where getting access to licenses and a test environment to build your products was either a credit card or PO purchase away, for us this was simply not the case. Fortunately, the Webex Developer team has created a no-cost Webex sandbox ([/docs/developer-sandbox-guide](https://developer.webex.com/docs/developer-sandbox-guide)) that removes a big barrier for startups to develop Webex apps. The only snag we ran into with the free sandbox was that there is only 1 account to really test the app with, but we were able to test our app within the Webex Meetings experience without any trouble as Webex meetings from the sandbox could have participants outside of the sandbox tenant join in.

### Challenges

Every journey has its challenges. Ours came in the form of Webex security features around personally identifiable information (PII). Webex is a secure platform, and it allows for PII to be enabled, or as we discovered, disabled. This capability has a direct impact on the availability of user information, for us, it was the user’s email address, with PII disabled the email address was no longer available through the Webex SDK to our embedded app. It's essential to note that these challenges were primarily due to our architectural considerations, not the limitations of the Webex platform. In the end, this hurdle helped us hone our app, allowing us to cater to diverse use cases where PII wasn't available.

### From Sandbox to Certification: A Smooth Ride

The certification process, often feared by developers, was where Webex's partnership shone brightly. Armed with the insights from their comprehensive documentation and assisted by the stellar Webex app team, we sailed through this phase. Their patience and guidance ensured our app was ready to provide a top-notch experience.

One important, headache-saving, piece of documentation that every company should follow when submitting their app is what is in [this blog post that Joe Zanini has put together](https://developer.webex.com/blog/hints-and-tips-for-submitting-an-app-to-the-webex-app-hub). The advice given here dramatically improves your chances of getting published to the Webex App Hub the first time you submit for approval increase exponentially.

### Golden Nuggets of Wisdom

For fellow developers venturing into the Webex ecosystem, here's my advice:

1. Tap into Webex's Resources: The provided documentation and SDK are your best friends. They'll guide you through the process like a trusted compass.
1. Embrace Communication: The Webex Developer Team is there for you. Their responsiveness over email and their commitment to assisting you is a game-changer.
1. Crucial Read: [Joe’s blog](https://developer.webex.com/blog/hints-and-tips-for-submitting-an-app-to-the-webex-app-hub): So good I thought I would mention it twice!

In conclusion, developing the PitchHub Teleprompter App for the Webex App Hub was an exhilarating journey. The process for building and publishing Webex apps is a well-oiled machine and major kudos to the Webex Developer Team.

Together, let's continue to innovate, inspire, and elevate the art of presentation.

Cheers,

-Cary

Chief Product Officer, PitchHub
