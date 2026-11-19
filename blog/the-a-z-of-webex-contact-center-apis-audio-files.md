---
type: Article
title: 'The A-Z of Webex Contact Center APIs: Audio Files'
canonical_url: https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-audio-files
content_type: blog
date: '2025-04-17'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-a-z-of-webex-contact-center-apis-audio-files)

Thank you for checking out the third installment of the blog series, “The A-Z of Webex Contact Center APIs”. This is the series where we are attempting to traverse the vast set of RESTful API endpoints available for Webex developers. In this edition we will be going over the Audio Files APIs and how audio files are used in the Webex Contact Center ecosystem. 

### Webex Contact Center Audio Files

Webex Contact Center administrators will strategically use [audio prompts](https://help.webex.com/en-us/article/be12vp/Manage-audio-files#concept-template_d1a97755-4e53-4993-a65f-9859a2134332), [custom agent greetings](https://help.webex.com/en-us/article/be12vp/Manage-audio-files#concept-template_10502595-49be-4026-94c8-c5de36f2f03d), and [courtesy callback](https://help.webex.com/en-us/article/n5595zd/Webex-Contact-Center-Setup-and-Administration-Guide) messages throughout the [Flow Designer](https://help.webex.com/en-us/article/nhovcy4/Build-and-manage-flows-with-Flow-Designer) setup and routing configuration process.

### Audio File Management

There are various options for Webex Contact Center users to manage audio files in the system. ####  

#### The Control Hub

The Webex Control Hub is a web-based, central management portal that allows Webex administrators to manage a Webex organization, users, assign services, view analytics, and more. Because the Control Hub is the mothership for the entire Webex Suite (Messaging, Meeting, Calling, Vidcast, Contact Center, Connected UC and Hybrid Services), the following material will focus on the Webex Contact Center use case. It can be easy to get caught up in managing [announcement audio files for Webex Calling](https://help.webex.com/en-us/article/n5y120ab/Manage-announcement-repository) and the APIs mentioned in this blog will not populate audio files for that service.

To manage Webex Contact Center audio files using the Control Hub, start by signing in at admin.webex.com as an administrator. Then go to Services > Contact Center > Customer Experience > Audio Files. Here an administrator can create and upload new audio files. Also, they can update and delete existing files.

#### Third Party Integrations

One of the benefits of being a Webex Contact Center user is that there is a robust set of open RESTful APIs available for teams to use to build apps that automate the heavy lifting when it comes to migrating from say an on-prem contact center solution to a cloud-based solution like the Webex Contact Center. One such application is [Univonix CC Accelerator](https://apphub.webex.com/applications/univonix-cc-accelerator-uccx-to-webex-contact-center-univonix). This tool automates UCCX Discovery and Migration to the Webex Contact Center. The service is a set of tools designed to streamline the migration process by automating data provisioning, thus accelerating time to consumption. You can see more information about this integration, and many more, on the Webex App Hub.

#### Internal Tools for Automation

Some organizations have technical talent on various teams that help automate processes like migration or build internal tools for managing files. The developer docs on the Webex developer portal are awesome, but sometimes it helps to learn about a developer’s experience with the tools of the task when approaching a new project. That is why this blog series exists, to give developers a glimpse of what happens beyond what is documented.

### Audio Files APIs

Let’s break down the API endpoints that make audio file magic happen:

#### Create a New Audio File

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/create-a-new-audio-file](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/create-a-new-audio-file)

The [Create a New Audio File API](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/create-a-new-audio-file) is self-explanatory. This is the endpoint a developer is going to use when building apps for uploading new files to the audio file library. This API also will be used in migration applications. Integrations will require an administrators access token and the `cjp:config` scope.

There are some caveats that are worth noting when implementing this API call. For example, the documentation calls for two objects to be sent in the body of the request, audioFileInfo and audioFile. The audioFileInfo object is a JSON object that contains things like the file name, the Webex organization id, the file content type (AUDIO_WAV, AUDIO_X_WAV), an optional blob id, download URL, and description. The audioFile is a binary representation of the file data.

The audioFileInfo JSON object is pretty straight forward but there are some things to consider when building it. For example, the `id`, `createdTime`, `lastUpdatedTime`, and `url` are optional parameters to include, but a developer does not want to include a value for these when initially creating or uploading an audio file via API because the Webex Contact Center system will build these on a successful upload. The audioFile object must be binary. A developer is not limited when it comes to file to binary conversion methods. See the below sample code for an idea of how one can accomplish this conversion.

When both objects are compiled, the developer can then use a form data interface to construct a set of key/value pairs representing form fields and their values that are then consumed by Webex Contact Center. Below is a sample of how to implement this API using JavaScript, on a Node server.

```javascript
import axios from 'axios'
import FormData from 'form-data';
import fs from 'fs';
import path, { resolve } from 'path';
import { fileURLToPath } from 'url';

const __filename = fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);

/*
a helper function for writing a file that was passed locally to 
later be read/converted into binary.
*/
function writeFileLocally(file) {
    return new Promise((resolve, reject) => {
      const tempFilePath = path.join(__dirname, file.file.originalname);
      fs.writeFile(tempFilePath, file.file.buffer, (err) => {
        if (err) {
          reject(err);
        } else {
            resolve(tempFilePath);
        }
      });
    });
}

/*
a function to be used in other parts of the backend. takes in a file
and a user/administrator object.
*/
export const createAudioFileApi = async function (file, user) {
    //prep form data
    const formData = new FormData();
    //construct JSON object to serve as audioFileInfo in API call.
    const fileInfo = {
      name: file.name,
      contentType: 'AUDIO_WAV',
      systemDefault: false
    }
  
    const writeFile = await writeFileLocally(file);
    //attach audioFile binary to formData
    formData.append('audioFile', fs.createReadStream(writeFile), {
      contentType: 'audio/wav'
    });
    //attach audioFileInfo JSON object to formData
    formData.append('audioFileInfo', JSON.stringify(fileInfo), {
      contentType: 'application/json'
    });
    //sample API call
    const response = await axios.post(`https://api.wxcc-us1.cisco.com/organization/${user.orgId}/audio-file`, formData, {
      headers: {
          'Accept': '*/*',
          'Authorization': `Bearer ${user.accessToken}`
      }
  }).catch(error => {
      if (error.response) {
        console.error('Request failed with status:', error.status);
        if (error.response.status === 404) {
          console.warn('Resource not found.');
        }
      } else if (error.request) {
        console.error('No response received:', error.request);
      } else {
        console.error('Error during request setup:', error.message);
      }
  
      return {
          success: false,
          message: error.message || 'An error occurred when accessing audio files.',
          code: error.code || 'AUDIO_FILES_ERROR'
      };
    });
  
    return response.data;
}
```

#### Update a Specific Audio File by ID

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/update-specific-audio-file-by-id](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/update-specific-audio-file-by-id)

Developers will use the [Update a Specific Audio File by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/update-specific-audio-file-by-id) if they want to do a complete overhaul of an existing audio file in the Webex Contact Center audio file library. The implementation is the same as the Create a New Audio File endpoint except that the id parameter, and desired updates, are required when calling this API. If the only desired change is something like the description, then a developer is advised to use the [Partially Update Audio File by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/partially-update-audio-file-by-id) endpoint as the implementation is more efficient.


#### Get Specific Audio File by ID

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/get-specific-audio-file-by-id](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/get-specific-audio-file-by-id)

Developers can use [Get Specific Audio File by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/get-specific-audio-file-by-id) to retrieve an existing Audio File in a given organization. In this API request developers should include the Webex Contact Center Organization ID and the audio file resource ID in the path parameters. Developers can also include an optional `includeUrl` query parameter to indicate whether they need the download URL.

#### Delete Specific Audio File by ID

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/delete-specific-audio-file-by-id](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/delete-specific-audio-file-by-id)

With the [Delete Specific Audio File by ID](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/delete-specific-audio-file-by-id), you guessed it, a developer can make a request, include Webex Organization ID and audio file resource ID information in the path parameters and delete a single audio file from the Webex Contact Center Audio File library.

#### Partially Update Audio File by ID

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/partially-update-audio-file-by-id](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/partially-update-audio-file-by-id)

This API was mentioned above. It is a lot simpler than not “partially” updating an audio file via API. The developer needs to include the Webex Organization ID and audio file resource ID information in the path parameters of the API request. In the body of the API call, the developer can include the changes to the description that are required and then look out for a successful response from the API server.

#### List References For a Specific Audio File

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-references-for-a-specific-audio-file](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-references-for-a-specific-audio-file)

A developer will maybe want to List [References For a Specific Audio File](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-references-for-a-specific-audio-file) before deciding if they want to delete this file. This API will provide some context to the extent in which an audio file is being used within a Webex Contact Center’s day to day operations. This API provides insight into which CAD variables in specific Flows are tied to the audio file. If there are many teams using the file, maybe to do some additional checks before changing a file for deleting it.

#### List Audio Files

[https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-audio-files](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-audio-files)

Developers can obtain a complete set of audio files contained by a Webex Contact Center Organization with the [List Audio Files](https://developer.webex.com/webex-contact-center/docs/api/v1/audio-files/list-audio-files) endpoint. This API will also return all data available about each audio file in the library.

#### Agent Personal Greeting Files

There is a brand-new set of APIs available for Webex Contact Center developers interested in zeroing in on audio files specifically for the Agent Personal Greetings feature. These APIs operate similarly to the Audio Files APIs except they will categorize the targeted files for this intended use case. You can check out the documentation [here](https://developer.webex.com/webex-contact-center/docs/api/v1/agent-personal-greeting).

### Need Some Help? We Got You Covered!

We are excited to provide you with support for these features. If you need help, the [Webex Developer Support Team](https://developer.webex.com/support) is standing by and happy to assist. You can also start or join a conversation on the [Webex for Developers Community Forum](https://cs.co/WebexDeveloperCommunity).
