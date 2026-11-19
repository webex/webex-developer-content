---
type: Article
title: AWS Public Cloud and Developer Associate Certification
canonical_url: https://developer.webex.com/blog/aws-public-cloud-and-developer-associate-certification
content_type: blog
date: '2022-09-30'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/aws-public-cloud-and-developer-associate-certification)

**Editor’s Note: Much of our blogs and documentation are centered on getting started with the Webex Developer Platform, but what happens when you are ready to deploy to production and submit to the **[Webex App Hub](https://apphub.webex.com/)**? This blog is about one Cisco engineer’s journey into the world of Amazon Web Services that many of our partners are using for their production integrations.**

Recently I took the AWS Developer Associate exam and can share a few thoughts about it and public cloud in general. For me, the main driver was to further explore how cloud works and get deeper hands-on experience. Before taking on the AWS exams, I only had a very limited understanding of the public cloud. How complex could it be, at the end of the day? You just put your application to a virtual server managed by someone, right? Right?

### The Cloud Practitioner Exam

Roughly a year before, I passed the AWS entry-level Certified Cloud Practitioner exam. At the time it was more like a sidecar to my DevNet Associate certification - I took both exams in one testing center visit. The CCP exam has proven to be pretty mind-opening - it turns out there are a lot of things going on in the cloud. It brushes broadly across about 30 AWS services with only a slight dive into a couple most foundational and important ones. It was mostly about memorization of what each service does. And while AWS has neat names for almost each of their services, not all of them are meaningful. On the other side, the Developer Associate goes in-depth into many of these services. I typically make brief handwritten notes when I study. My notes for the CCP exam fit on a couple sheets of paper. The Dev Associate exam took 53 sheets. Frankly, I did not expect that amount of content to be covered when I started to learn. But when you set a concrete goal, like a certification, it is much easier to be consistent and keep going over the hurdles.

### AWS Basic Services

So, is the cloud really that complex? Yes and no. There are many ways to use cloud resources. And indeed, you can just spin up a virtual machine (**EC2** instance) and put your application code onto it. But you can go in multiple directions beyond that. One is scaling - if your application is popular and needs to process a lot of requests, one VM, no matter how beefy it is, will not be able to cope with the traffic. At some point you won’t be able to scale vertically by reserving a more powerful VM. You’d need to scale horizontally by adding more instances or removing unused capacity according to load changes (**Auto Scaling Group**). A load balancer (**Elastic Load Balancer**) will need to be put in front of them to route the incoming requests.

Another direction - make your solution more cloud-native. Really, why should you care about the OS configuration, security patches and maintenance on your VMs? You only want your application to work. There are a few options you can use to make it happen - **Elastic Beanstalk** can create an appropriate environment for your applications by spinning up instances, configuring scaling and load balancing and so on.

### How CICD is Done with AWS

The industry best practice for many applications’ lifecycles is to implement small incremental changes frequently. This works especially well for web apps - your users usually “refresh” their app on every page load. With every code update, there will be a set of mandatory actions to be done, including module and integration testing, code deployment and environment swapping. With frequent updates, the more your update process is automated, the better. That’s when the practice of CICD (Continuous Integration/Continuous Delivery) comes into place. AWS has a bundle of tools to make it happen which can be used in unison or mixed with other, third-party tools:

- **CodePipeline** - a tool to build custom pipelines to orchestrate the CICD flow. You can define steps like pulling the code from a repository, building, testing, and deploying. All these may happen automatically but also a manual approval requirement may be defined.
- **CodeCommit** - software repository where your application code is stored. You can also use GitHub, GitLab, BitBucket or the like.
- **CodeBuild** - builds/compiles the code according to build instructions, which are usually bundled together with the code.
- **CodeDeploy** - helps to deploy the new build of the app to your infrastructure - VMs, containers, or Beanstalk environments, following a certain deployment tactic: all servers at once, rolling partial update, or blue-green environments.

&nbsp;

### Where to Deploy

When it comes to cloud infrastructure, the AWS Developer Associate exam goes significantly in depth of the infrastructure-as-code concept. AWS CloudFormation is a service you can use to define all your cloud infrastructure as a YAML text file. Having such a “template” file, you can spin up your cloud infrastructure in minutes. However, there is no easy way to automatically generate a YAML definition from your existing infrastructure. The CloudFormation format and specification is extensively covered in the exam.

Your infrastructure can also be containers, if the application was built with containerization in mind. AWS ECS - **Elastic Container Service** helps to run Docker containers and is well covered in the exam. ECS’s job is to run pieces of your application - “microservices” as tasks, make sure they are healthy, restart failed ones and orchestrate - make sure changes happen in the proper order. ECS is an AWS’s alternative to Kubernetes, but you can use Kubernetes in AWS too, with the EKS, **Elastic Kubernetes Service**. The Docker images of your containers can come from DockerHub or AWS's own alternative - **Elastic Container Registry**. To run the containers, some computational power needs to be provided - capacity. This can be done two ways - with the EC2 launch type by placing containers on your EC2 instances, and with the **Fargate** launch type which automatically scales the capacity, so you don’t have to worry about the instances.

### Going Serverless

You can go even further - go serverless. **AWS Lambda** and a set of other services can make it happen. To use Lambda, you break up your application logic into even smaller pieces (compared to containers) and implement each piece as a Lambda function. The function code just lives in the cloud and is run whenever the function is invoked. Functions can call other functions, make requests to other services and so on. For example, you may have one function that takes a request from the user and puts data in a database. Another function returns data from the database to the user. They do not really need to talk with each other directly.

In case you need to integrate some functions into a process, you can use various integration services, like SQS or SNS. **Simple Queue Service** helps to decouple parts of the application to allow asynchronous code execution, so one function does not have to freeze and wait until a downstream process is done with its job. SQS is said to be the oldest AWS service. Simple Notification Service lets one application send a message to multiple destinations following the pub/sub model. Useful in case you need a result of one function to be consumed by multiple others.

### Data Storage

Another big section of the exam is storage. You need some sort of storage outside of your “compute” part to help make services as stateless as possible. Thus, a loss of a server wouldn’t be a big deal - the data sits safely in a store. Just spin up a new instance and it’s good to go. Each AWS storage service has its own purpose, pros and cons, but here’s is a quick list:

- **Elastic Block Store** is like a USB stick connected to your instance: good for saving data of the instance but not that good to share data between many instances.
- **Elastic File System** - like a network attached drive, can be easily shared across many instances, and can store files centrally.
- **Simple Storage Service, S3** - a very popular and virtually unlimited object storage which does not require any provisioning. However, to store files in S3 you won’t be able to use standard file i/o calls; a specific to S3 API calls need to be made. To be fair, it’s not much harder than working with files, especially if you are using an AWS SDK.
- **Relational Database Service** offers a managed database service. You can run MySQL, PostgreSQL or other popular DBs without having to worry about maintenance. Amazon also offers Aurora - its proprietary database service, as part of RDS.
- **DynamoDB** is a NoSQL storage service from AWS. Throw JSON objects in it and read them back when needed. Works well in situations when you don’t have a complex data structure but need to move data fast and at great scale.

This is just a brief overview of more central services covered in the exam. There is also **ElastiCache** for data caching, **CloudFront** for content distribution, **Route 53** for DNS, **Kinesis** for data streaming, **CloudWatch** and **CloudTrail** for monitoring and auditing, and a whole bunch of security related services: **Identity and Access Management, Security Token Service, Key Management Service, NAT Gateways, Network ACLs** and many more.

### Wrapping Up

So, it seems like each service has its own purpose. And I must say, on CCP level they might feel redundant and overcomplicated, but the more you learn about possible use-cases, the more the existence of each service makes sense. AWS Developer Associate is a way more practical exam that connects the dots and makes you understand why it is built like that and how public cloud works.
