---
type: Article
title: Yarn Workspaces – Mono Repo and the Calling SDK
canonical_url: https://developer.webex.com/blog/yarn-workspaces-mono-repo-and-the-calling-sdk
content_type: blog
date: '2023-12-22'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/yarn-workspaces-mono-repo-and-the-calling-sdk)

Yarn Workspaces have become an essential tool in the developer's toolkit, revolutionizing the way we manage dependencies and structure our projects. In this comprehensive guide, we will explore the process of creating a Yarn Workspace, effectively managing scripts across packages within a workspace, running commands across multiple packages, listing all available workspaces, and weighing the pros and cons of using Yarn Workspaces.

Yarn workspaces follow a pattern called Monorepos, which can be used by various types of projects that require integration with Webex. Here are a few examples:

- **Unified Communications Applications:** These applications might offer a suite of communication and collaboration tools, integrating with Webex for video conferencing or messaging. A monorepo could be beneficial for managing the different modules of the app, like chat, file sharing, task management, and the Webex integration.
- **Customer Support Tools:** A customer support platform could integrate with Webex to provide real-time support through video calls. The monorepo could manage the various parts of the application, including ticketing system, user management, and the Webex integration.
- **Virtual Event Platforms:** For platforms hosting webinars or virtual conferences, integrating with Webex could provide a solution for live sessions. The monorepo would handle different aspects like event registration, content management, participant interaction features, and the Webex integration.
- **eLearning Platforms:** Such platforms may use Webex integration to conduct live classes or lectures. A monorepo can be useful in managing different components like course management, student databases, assessment tools, and the Webex integration.
- **Project Management Tools:** Project management software might integrate with Webex to facilitate team collaboration. In this case, a monorepo can provide a unified codebase for features like task tracking, resource allocation, reporting, and the Webex integration.

<br/>

### Creating a Yarn Workspace

Now, let's walk through the steps of creating a Yarn Workspace for your project.

#### Initialize a Yarn Repository

Use the following command to initialize a Yarn Workspace with default options quickly:

```bash
>> yarn init -y
yarn init v1.22.19
warning The yes flag has been set. This will automatically answer yes to all questions, which may have security implications.
success Saved package.json
✨  Done in 0.01s.
```

The `yarn init -y` command initializes a Yarn project with default options, saving you from answering a series of questions. 

#### Add Packages

To add packages to your workspace, navigate to the root directory and create a folder `meetings-sdk`. In this folder, initialize a yarn repo as mentioned above.

Here's what the `meetings-sdk/package.json` will look like:

```json
{
  "name": "meetings-sdk",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "echo \"Package script executed successfully\" && exit 0",
    "test": "jest"
  },
  "dependencies": {
    // Your dependencies here
  }
}
```

#### Updating the Root package.json

Update the `package.json` in the root folder to include the `meetings-sdk` package as a workspace and mark the `webex` package as `private`. This is because Yarn Workspaces work only with private packages.

Here's how the `package.json` in the root folder will look like:

```json
{
  "name": "webex",
  "version": "1.0.0",
  "main": "index.js",
  "private": true,
  "workspaces": [
    "meetings-sdk"
  ],
  "scripts": {
    // Your scripts here
  },
  "dependencies": {
    // Your dependencies here
  }
}
```



> **Info**
>
> Once this is done, please do `yarn install` in the root folder of the monorepo. This ensures all the mentioned packages are marked as a workspace



### Managing Scripts in Yarn Workspaces

Yarn Workspaces provide a convenient way to manage and execute scripts across packages. Here's how you can do it:

#### Creating Scripts

In each package's `package.json` file, define the scripts you want to execute. For example:

```json
"scripts": {
  "start": "echo \"Package script executed successfully\" && exit 0",
  "test": "jest"
}
```

#### Executing Scripts from the Root

To execute the "start" script from the root of the project, use the following command:

```bash
>> yarn workspace meetings-sdk start
yarn workspace v1.22.19
yarn run v1.22.19
$ echo "Package script executed successfully" && exit 0
Package script executed successfully
✨  Done in 0.03s.
```

#### Running Commands Across Multiple Packages

Yarn provides the foreach command to run the same command across multiple packages. For example, to run the "start" script in all packages, you can use:

```bash
>> yarn workspaces run start
```

This will execute the "start" script in every package within the workspace.

#### Listing Yarn Workspaces

To list all available workspaces, use the following command:

```bash
>> yarn workspaces list
➤ YN0000: meetings-sdk
➤ YN0000: Done in 0s 2ms
```

### Using Yarn Workspaces in Another Workspace

Yarn Workspaces provide a powerful mechanism for sharing code and dependencies among packages within a monorepo. If you have multiple Yarn workspaces and need to use code from one workspace in another, follow these steps:

#### Setting up the Dependency

Let's say you have two workspaces, `meetings-sdk` and `calling-sdk`. If `calling-sdk` needs to use code from `meetings-sdk`, you need to set up the dependency. Go to `calling-sdk/package.json` and add a dependency attribute that looks like the below code:

```json
{
  "name": "calling-sdk",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "echo \"Package script executed successfully\" && exit 0",
    "test": "jest"
  },
  "dependencies": {
    "meetings-sdk": "workspace:^",
  }
}
```



> **Info**
>
> Once the above step is complete, do yarn install. This ensures that the `meetings-sdk` workspace is rightly linked to the `calling-sdk` workspace.



#### Using the Linked Package

Now that `calling-sdk` is linked to `meetings-sdk`, you can import and use modules from `meetings-sdk` within `calling-sdk` as if they were regular dependencies.

For example, in a file within `calling-sdk`, you can do:

```javascript
// In calling-sdk/src/index.js
import { someFunction } from 'meetings-sdk';
```



> **Info**
>
> These packages can simply be unlinked by removing the dependency in the respective package.json and following it up with a `yarn install`.



### Pros

There are a variety of pros to using Yarn Workspaces.

#### Dependency Management

Yarn Workspaces excel in simplifying dependency management. With a single `node_modules` folder at the root, dependencies are hoisted, reducing redundancy, and ensuring consistency across packages.

#### Improved Local Development

Yarn Workspaces enhance the local development experience by allowing developers to work on multiple packages simultaneously. Changes in one package are reflected immediately, streamlining the debugging and testing process.

#### Ease of Code Sharing

Yarn Workspaces promote code sharing among packages. Shared modules or utilities can be developed and maintained centrally, encouraging a modular and maintainable codebase.

#### Tooling Flexibility

Yarn Workspaces can be set up such that the tooling can work together or separately. For instance, in the same mono repo, one package shall use Jest for unit testing while another can use mocha and still manage dependency 

### Cons

On the other hand, be sure to keep in mind the cons.

#### Learning Curve

Adopting Yarn Workspaces might be a bit difficult for developers who are unfamiliar with the tool. Understanding how hoisting works and managing workspace-specific configurations can take some time.

#### Potential Overkill for Small Projects

For small projects with minimal dependencies, Yarn Workspaces might be an overkill.

### The Calling SDK

In the Webex Developer Platforms group, our [Webex Web SDK](https://github.com/webex/webex-js-sdk) is a mono repo that uses Yarn workspaces effectively. It is relatively a large codebase and movement to Webex Web SDK provided the flexibility of having separate tools for each package. This way, we were able to migrate the Calling SDK from a separate repository into the public repository without having to change any of its existing toolsets. 

The Calling SDK offers a variety of features such as Calling, Contacts, and Voicemail etc., To get started with the calling SDK, please head over to this Wiki: [Developer Portal – Webex Calling SDK](https://developer.webex.com/docs/sdks/webex-calling-sdk)

### Conclusion

Yarn Workspaces offer a powerful solution for managing mono repositories, streamlining development workflows, and optimizing CI/CD pipelines. However, their adoption comes with a learning curve and might be more beneficial for larger projects with complex dependencies. It's crucial to weigh the pros and cons and assess the specific needs of your project before deciding to implement Yarn Workspaces.
