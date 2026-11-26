---
type: Excerpt
canonical_url: https://developer.webex.com/docs/basics
lane: production
source_revision: cms-sha256:7997d2fd5360eb5070f70ceccfec1a51ace552539abb500c374ddbf156561fd4
publication_state: verified_published_snapshot
heading_hierarchy:
- Message Attachments
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/basics). [Full Markdown](../../../../docs/basics.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

While working with the Webex REST API is easy, there are a few things we standardize on throughout the API, such as pagination of long result sets or HTTP response codes.

## Selected section

## Message Attachments

Webex has native support for posting messages with file attachments. Using the [Messages API](https://developer.webex.com/docs/api/v1/messages) you can send messages containing text, text with attachments, or just share a file with the room without any text. Message attachments are limited to 100MB each.

What you may not know is that Webex has special support for most PDFs, Microsoft Word, Microsoft Excel, Microsoft PowerPoint, and most popular image formats. For these file types, Webex clients will render a preview in the room and a full view when clicked.

Here is the complete list of supported file types and extensions:

- Microsoft Word (doc, docx)
- Microsoft Excel (xls, xlsx)
- Microsoft PowerPoint (ppt, pptx)
- Adobe Portable Document Format (pdf)
- JPEG (jpg, jpeg)
- Windows Bitmap (bmp)
- Graphics Interchange Format (gif)
- Portable Network Graphics (png)

### Send a Message with Attachments

#### Local File Attachments

To send local file attachments, simply post a message by including your access token in the `Authorization` header and the path to your local file with the `files` parameter. Optionally, you can also include a plain-text message with the attachment by using the `text` parameter. When uploading files directly from your local filesystem, your request will need to be a `multipart/form-data` request rather than JSON. Here's an example of using cURL to send a new message with a local file as a file attachment:

```bash
curl --request POST \
  --header "Authorization: Bearer ACCESS_TOKEN" \
  --form "files=@/home/desktop/example.png;type=image/png" \
  --form "roomId=Y2lzY2....." \
  --form "text=example attached" \
  https://webexapis.com/v1/messages
```

You can also use your favorite scripting language to send messages with local files. Here's an example of using Python with a local file:

```python
import requests
from requests_toolbelt.multipart.encoder import MultipartEncoder

m = MultipartEncoder({'roomId': 'Y2lzY2.....',
                      'text': 'example attached',
                      'files': ('example.png', open('example.png', 'rb'),
                      'image/png')})

r = requests.post('https://webexapis.com/v1/messages', data=m,
                  headers={'Authorization': 'Bearer ACCESS_TOKEN',
                  'Content-Type': m.content_type})

print r.text
```

#### Remote Attachments

Alternatively, if you have a file available via a publicly-accessible URL that you wish to share, you can use the URL as the value in the `files` JSON parameter instead of attaching your local file in a multipart message. The `files` parameter currently takes one URL as an input. A plain-text message can also be included in the `text` parameter. Here's an example of using cURL to send a new message with a remote file as a file attachment:

```bash
curl --request POST \
  --header "Authorization: Bearer ACCESS_TOKEN" \
  --header "Content-Type: application/json" \
  --data '{"roomId":"Y2lzY2.....","text":"Example file","files":["http://www.example.com/images/media.png"]}' \
  https://webexapis.com/v1/messages
```

### Retrieve Message Attachments

#### Retrieving Message Details

In order to retrieve the file details such as `filename` and `content-type`, you can simply use a HEAD request with your access token in the `Authorization` header. This is particularly useful if you just want to verify the filename and type before downloading the content.

```bash
curl -I https://webexapis.com/v1/contents/Y2lzY...... -H "Authorization: Bearer ACCESS_TOKEN"

HTTP/1.1 200 OK
Cache-Control: no-cache
Content-Disposition: attachment; filename="example.png"
Content-Length: 44752
Content-Type: image/png
```

#### Retrieving Message Attachments

Files attached to a message are returned in the `files` property of the [message](https://developer.webex.com/docs/api/v1/messages) object. To retrieve one of these files you should issue a `GET` request on the file URL including your Access Token in the `Authorization` header.

```bash
curl -H "Authorization: Bearer ACCESS_TOKEN" https://webexapis.com/v1/contents/Y2lzY......
```

### Anti-Malware Scanning

Organizations may enable [anti-malware scanning of files](https://help.webex.com/yr6g4bb/) in Webex to protect users from malicious files.

If a file is subject to evaluation, it will be quarantined and scanned. While the file is under evaluation, requests to retrieve the file will fail with a `423 Locked` HTTP response. A `Retry-After` header in the response will indicate when the request should be attempted again. There is no guarantee that the malware scan will have finished during the retry interval and you may need to retry again. The retry-after time is aligned with the majority of scans that are done on an average basis.

Infected files will be unavailable for download. Requests to retrieve a file that was scanned and found to be infected will fail with a `410 Gone` HTTP response.

Requests for files that a not scannable - for example encrypted files - will get a `428 Precondition Required` response. Adding the query parameter `allow=unscannable` to the request will meet the precondition and enable the request to be fulfilled. The user assumes all risks associated with these files.
