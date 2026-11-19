---
type: Article
title: 'Robert Heath Case Study: Webex Cloud'
canonical_url: https://developer.webex.com/blog/robert-heath-case-study-webex-cloud
content_type: blog
date: '2023-09-12'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/robert-heath-case-study-webex-cloud)

Robert Heath is a family owned and managed heating business in New Malden, England that has been in continuous operation for almost forty-five years (incorporated in 1979). During that time, Robert Heath has grown from a local heating installation company to one of the leading energy specialists in the United Kingdom. Providing services to large and small landlords, their core client base is within the non-profit, social housing space, but they also handle other large clients such as the UK public sector. As they explain:

>Our mission is to ensure that our affordable energy solutions evolve to meet the changing needs of our customers, while maintaining our reputation for the highest quality of service.

When thinking of heating contractors, the prevailing image is one of small, home-grown systems relying on standard telephony solutions for customer communication and employee dispatch along with a basic and most likely, manual scheduling system. However, Robert Heath has adopted a technology focused approach, from their [web site](https://robertheath.co.uk/):

>Our company has a proud heritage, but we’re always looking toward the future. Technology is at the forefront of everything we do. We are frequently redefining standards in a resistive industry. Robert Heath Heating pioneered the use of online gas safety records in the UK. Continually innovating and harnessing the power of technology to provide outstanding service across the board.

### The Challenge

As with many companies working in such "resistive industries" Robert Heath initially found itself at the mercy of a legacy Avaya system during its initial Cisco integration which started in earnest in 2011. The Avaya system, while functional, focused on a traditional telecom infrastructure, and as Michael Heath, Managing Director describes, "Almost all employees are remote or mobile so manageability and being able to deliver a solution at scale was critical."

During the first phase of their transition to Cisco technologies, over the course of six months working with Ionize Ltd., Robert Heath Heating implemented an on-premise solution based on Cisco® Borderless Network architecture including three Cisco 2900 Series Integrated Services Routers supporting session initiation protocol (SIP) trunking and ISDN traffic, along with one Cisco 1900 Series Integrated Services Router as well as switching equipment and a variety of Cisco security appliances. From an interface point of view, phase one utilized Jabber® instant messaging, supporting point to point video calls as well as multiple access methods, from desktop browsers to mobile applications.

However, Jabber’s lack of messaging continuity as well as single sign on support, made usage cumbersome. Since the Jabber solution was limited to a single location, only a subset of their 350 to 400 employees had access to the full range of communication services, negatively affecting engagement. Furthermore, system maintenance was a challenge: on-premise equipment, employee machines and operating systems had to be monitored, diagnosed, and fixed when necessary, and it was impossible to easily deploy Jabber updates across the workforce

Although the phase one migration had been a resounding success compared to the Avaya system, Robert Heath determined that there was still room for considerable improvement and decided that a phase two was necessary: a transition from the Cisco on-premise system to Webex Cloud.

### Seamless Migration to Webex Cloud

Starting in May 2021, Robert Heath began its migration away from its on-premise solution to Webex Cloud. The best thing about the migration from the Jabber-based solution to the Webex Cloud solution was that there was practically no transition for users. With a single sign on to a single system, everything "just worked." As Michael Heath describes,

>Even in front of my PC, I could be on the road and having the messaging, all the conversations synced up between all the devices—what feels like a really simple thing—is something that really, really helped in terms of the way we do business.

Compelling benefits for the new Webex solution include:

- Fully indexed and searchable information for every customer interaction.
- Easy device provisioning with no extra administrative steps—full user self-service.
- Effortless updates to a single app across all supported devices.
- Automatic retention policies.
- Seamless syncing between all devices.
- Single sign on integrated with Cisco Duo.

Other benefits include that the calls to customers are proxied through the main Robert Heath telephone number, meaning that calls from technicians are much less likely to be ignored as opposed to private individual cell phone numbers. And, most importantly, Webex logging capabilities solve the complicated legal compliance requirements requiring contractors to prove that they’ve followed all the necessary steps to remedy a particular problem: recording and logging calls on legacy networks requires complex coordination between providers but Webex Calling handles that requirement natively and transparently.

One aspect of the development process that stood out to Robert Heath is that the quality of the Webex API documentation is high and the ability to try out functions directly from within the Developer Portal is a significant benefit. According to Kristian Ellmore, Robert Heath’s Director of Information Communication Technology, "You don’t even have to be a developer to understand much of the API functionality. That means that rather than *talking* about implementing features, those features are **actually getting implemented**."

### Webex Integration Details

When working with gas and electrical appliances, in the winter when the hot water goes down, for example, diagnostic speed and accuracy are critical. Once a technician is dispatched it’s of vital importance that any errors or roadblocks are caught early and addressed immediately. Robert Heath’s Webex integration enables errors and issues to be caught and flagged *immediately as they occur*, avoiding costly re-routing and re-scheduling—instead of sending a technician back on a separate trip the next day to address a problem, the technician can be notified before they’ve even left the immediate area.

Robert Heath’s Webex solution centers on the creation of ad-hoc Webex spaces for each customer incident, via a custom Webex bot. The bot creates the space and then automatically populates it with the necessary administrative and technical employees depending on the nature of the incident. All incident communication takes place within the space and all information from each incident is logged, and only when the incident is completely resolved, are the members released and the space deleted.

Other automated features of Robert Heath’s solution include:

- Real-time notifications which are extended to their ERP platform.
- Checking for and flagging duplicate jobs.
- Checking for and flagging missing information.

The key focus of the solution, then, is creating a Webex space containing all the **necessary stakeholders** along with all the **necessary context** for those stakeholders to make decisions that can **mitigate the problem in as short a time as possible**.

### Application workflow examples

In this section, we’ll highlight typical workflows in which issues are intercepted and addressed using the Robert Heath Webex Cloud implementation.

#### Incomplete job submission

In this case, a Webex space is created with the necessary stakeholders including the relevant manager for the technician. The CSM bot reports on the error and offers options to view the job or contact the engineer via Webex (**Webex Engineer**):

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt7490343e6ca17f0e/64f88122ec9337aab4ec4fd6/robert-heath-case-study-1.png)

In this case, the technician hasn’t uploaded a photo of the completed job which is a compliance requirement. The manager tagged in the Webex space can contact the engineer directly to take remedial action before they’ve left the site as well as view the specifics of the job itself.

#### Missing certificate details

Specific work certifications require their own specialized metadata and information. Here, the technician has omitted critical data:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt87771157806b01a4/64f88122a8cf8b75213de2b3/robert-heath-case-study-2.png)

The CSM Bot’s Card enables the technician to easily provide the required information via an intuitive card interface, and, once entered, the data is passed back to dynamically update the certificate.

#### Unable to access a property

In the next incident, the technician has been unable to access the property:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt759eb93ccc368152/64f88123e64971e43e690494/robert-heath-case-study-3.png)

Again, a space is created with the necessary stakeholders and a set of options is offered to the technician’s manager who can:

- View the details of the job.
- Rebook the same engineer.
- Email the client to resolve the access problem. Note that an editable email template is automatically included.
- Tag the incident as reviewed to wait for further developments.

<br/>

#### Intercepting a high-risk issue

In this case a gas service technician has encountered a safety hazard involving an unsafe gas boiler:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltf1987f4be4c93d93/64f88122c12d774b60d04892/robert-heath-case-study-4.png)

A Webex space is opened that **cannot be deleted** until the issue is resolved. The technician’s manager can handle contacting the client, getting the necessary access, and resolving the situation ASAP.

#### Personnel management

A dedicated logging space for technicians and managers indicates the status of any engineers who have not yet requested jobs, for purposes of load balancing and time management:

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/blt5202f0dce447dc91/64f88122ea4b5d8de7510427/robert-heath-case-study-5.png)

### Plans for the future

Robert Heath’s plans don’t stop with their customer incident automation, however, and they’re already actively planning phase 3. With more than 25 thousand calls a month and a high number of on-site visits, ensuring frictionless customer service engagements is critical, as is minimizing expensive truck rolls.

Using [Webex Contact Center](https://help.webex.com/en-us/landing/ld-sxjj9p-WebexContactCenter/Agent), their solution can expand to the beginning-to-end automation of call routing. Custom Contact Center logic can automatically route calls to most suitable technician, completely bypassing an interim customer service rep. In cases where there isn’t enough context, simple push button interfaces can be created so that service advisers can easily address the most common situations. In addition, licensed support for Webex Meetings allows people in a space to easily start full video meetings with all key personnel, which saves time and effort for persons on mobile devices where typing can be a challenge.

As Kristian Ellmore points out, "the surprising thing is that those integration capabilities were completely unexpected, and only came to light after investing in the Webex platform."
