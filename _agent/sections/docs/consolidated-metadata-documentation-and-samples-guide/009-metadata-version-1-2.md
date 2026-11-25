---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd
publication_state: verified_published_snapshot
heading_hierarchy:
- metadata version 1.2
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

## metadata version 1.2

Metadata version 1.2 introduces two new fields in `serviceData`: `connectedParty` and `managedBy`. The following samples demonstrate these fields across various calling scenarios.

`answererInfo` is deprecated starting with metadata version `1.2` and should not be expected in version `1.2` payloads.



#### Scenario: Outbound Call with Connected Party

This example shows an outbound call where the `connectedParty` field captures the identity of the remote connected party.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8wYjFhNmQ3MC0yMDk2LTRkMTctOTgxZS0yMjdkMjNlMTkzMmE",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xYjU2MDVjYS1lMjMwLTQzMzAtYjVhYy1hZDEwMmNhMTg4NjA",
  "ownerType": "USER",
  "ownerName": "Test User",
  "ownerEmail": "testuser@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "0b1a6d70-2096-4d17-981e-227d23e1932a",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "f8a2b3c4-d5e6-7890-abcd-ef1234567890",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8xYjU2MDVjYS1lMjMwLTQzMzAtYjVhYy1hZDEwMmNhMTg4NjA",
        "email": "testuser@example.com"
      },
      "number": "5001",
      "name": "Test User"
    },
    "calledParty": {
      "actor": null,
      "number": "+14085551234",
      "name": ""
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "External User"
    },
    "callId": "callhalf-123456789:0",
    "session": {
      "startTime": "2025-03-15T10:30:00Z",
      "stopTime": "2025-03-15T10:35:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Inbound Call with Connected Party

This example shows an inbound call where the `connectedParty` field refers to the identity of the caller that is connected.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8xYTJiM2M0ZC01ZTZmLTdhOGItOWMwZC1lZjEyMzQ1Njc4OTA",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8yYzM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
  "ownerType": "USER",
  "ownerName": "Alice Smith",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "1a2b3c4d-5e6f-7a8b-9c0d-ef1234567890",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085559876",
      "name": "External Caller"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8yYzM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
        "email": "alice@example.com"
      },
      "number": "5002",
      "name": "Alice Smith"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085559876",
      "name": "External Caller"
    },
    "callId": "callhalf-987654321:0",
    "session": {
      "startTime": "2025-03-15T11:00:00Z",
      "stopTime": "2025-03-15T11:10:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Shared Line with Managed By

This example demonstrates the `managedBy` field for a shared line scenario, indicating the device owner who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
  "ownerType": "USER",
  "ownerName": "Bob Johnson",
  "ownerEmail": "bob@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "3d4e5f6g-7h8i-9j0k-1l2-m3n4o5p6q7r8",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS80ZTVmNmc3aC04aTlqLTBrMWwtMm0zbi00bzVwNnE3cjhzOQ",
        "email": "carol@example.com"
      },
      "number": "5003",
      "name": "Carol Davis"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS8zZDRlNWY2Zy03aDhpLTlqMGstMWwyLW0zbjRvNXA2cTdyOA",
        "email": "bob@example.com"
      },
      "number": "5004",
      "name": "Bob Johnson"
    },
    "connectedParty": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS80ZTVmNmc3aC04aTlqLTBrMWwtMm0zbi00bzVwNnE3cjhzOQ",
        "email": "carol@example.com"
      },
      "number": "5003",
      "name": "Carol Davis"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS81ZjZnN2g4aS05ajBrLTFsMm0tM240by01cDZxN3I4czl0MA",
        "email": "manager@example.com"
      },
      "number": "5005",
      "name": "Line Manager"
    },
    "callId": "callhalf-112233445:0",
    "session": {
      "startTime": "2025-03-15T14:00:00Z",
      "stopTime": "2025-03-15T14:15:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Virtual Line with Managed By

This example shows a virtual line scenario where `managedBy` indicates the device owner who handled the call on behalf of the virtual line.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1ZJUlRVQUxfTElORS82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0",
  "ownerType": "VIRTUAL_LINE",
  "ownerName": "Sales Hotline",
  "ownerEmail": "sales@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "6f7g8h9i-0j1k-2l3m-4n5o-6p7q8r9s0t",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "c3d4e5f6-a7b8-9012-cdef-345678901234",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085557777",
      "name": "Customer"
    },
    "calledParty": {
      "actor": {
        "type": "VIRTUAL_LINE",
        "id": "Y2lzY29zcGFyazovL3VzL1ZJUlRVQUxfTElORS82ZjdnOGg5aS0wajFrLTJsM20tNG41by02cDdxOHI5czB0"
      },
      "number": "8001",
      "name": "Sales Hotline"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085557777",
      "name": "Customer"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS83aDhpOWowLTFrMmwtM200bi01bzZwN3E4cjlzMHQxdTI",
        "email": "salesrep@example.com"
      },
      "number": "5010",
      "name": "Sales Representative"
    },
    "callId": "callhalf-556677889:0",
    "session": {
      "startTime": "2025-03-15T15:30:00Z",
      "stopTime": "2025-03-15T15:45:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": []
  }
}
```

#### Scenario: Call Queue with Agent as Recording Owner

This example shows a call queue scenario where a call is routed to a call queue and answered by an agent. The recording owner is the agent, and `managedBy` indicates the agent who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
  "ownerType": "USER",
  "ownerName": "Agent Smith",
  "ownerEmail": "agent.smith@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "9a0b1c2d-3e4f-5a6b-7c8d-9e0f1a2b3c4d",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "d4e5f6a7-b8c9-0123-defg-456789012345",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "Customer"
    },
    "calledParty": {
      "actor": {
        "type": "CALL_QUEUE",
        "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
      },
      "number": "8000",
      "name": "Support Queue"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085551234",
      "name": "Customer"
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
        "email": "agent.smith@example.com"
      },
      "number": "6001",
      "name": "Agent Smith"
    },
    "callId": "callhalf-998877665:0",
    "session": {
      "startTime": "2025-03-15T16:00:00Z",
      "stopTime": "2025-03-15T16:12:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-03-15T16:00:00Z",
        "mediaStreams": [
          {
            "streamId": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "p1a2b3c4-d5e6-f7a8-b9c0-d1e2f3a4b5c6",
            "name": "Agent Smith",
            "number": "6001",
            "actor": {
              "type": "USER",
              "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS85YTBiMWMyZC0zZTRmLTVhNmItN2M4ZC05ZTBmMWEyYjNjNGQ",
              "email": "agent.smith@example.com"
            },
            "aor": "sip:agentsmith@******",
            "send": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "123456789"
              }
            ]
          },
          {
            "id": "p2b3c4d5-e6f7-a8b9-c0d1-e2f3a4b5c6d7",
            "name": "Customer",
            "number": "+14085551234",
            "actor": null,
            "aor": "sip:+14085551234@X.X.X.X;user=phone",
            "send": "f1e2d3c4-b5a6-9807-6543-210fedcba987",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "987654321"
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "6001",
          "origCalledNumber": {
            "actor": {
              "type": "CALL_QUEUE",
              "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
            },
            "number": "8000"
          },
          "numOfRedirections": 1
        },
        "acd": {
          "actor": {
            "type": "CALL_QUEUE",
            "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MA"
          },
          "acdName": "Support Queue",
          "acdNumber": "8000"
        },
        "announcementData": null
      }
    ]
  }
}
```

#### Scenario: PSTN Caller to Call Queue with Call Queue as Recording Owner

This example shows a PSTN caller calling a Call Queue. The recording owner is the Call Queue, and `managedBy` indicates the agent who handled the call.

```json
{
  "id": "Y2lzY29zcGFyazovL3VzL1JFQ09SRElORy8xMjM0NTY3OC1hYmNkLWVmMTItMzQ1Ni03ODkwYWJjZGVmMTI",
  "orgId": "Y2lzY29zcGFyazovL3VzL09SR0FOSVpBVElPTi8xZWI2NWZkZi05NjQzLTQxN2YtOTk3NC1hZDcyY2FlMGUxMGY",
  "ownerId": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q",
  "ownerType": "CALL_QUEUE",
  "ownerName": "Customer Support Queue",
  "ownerEmail": null,
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.2",
  "serviceData": {
    "callRecordingId": "12345678-abcd-ef12-3456-7890abcdef12",
    "locationId": "Y2lzY29zcGFyazovL3VzL0xPQ0FUSU9OLzEyMzQ1Njc4OTBhYmNkZWY",
    "callSessionId": "e5f6a7b8-c9d0-1234-efgh-567890123456",
    "personality": "terminator",
    "callingParty": {
      "actor": null,
      "number": "+14085559999",
      "name": ""
    },
    "calledParty": {
      "actor": {
        "type": "CALL_QUEUE",
        "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
      },
      "number": "8000",
      "name": "Customer Support Queue"
    },
    "connectedParty": {
      "actor": null,
      "number": "+14085559999",
      "name": ""
    },
    "managedBy": {
      "actor": {
        "type": "USER",
        "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hZ2VudDEyMzQ1Njc4OTBhYmNkZWYxMjM0",
        "email": "agent.johnson@example.com"
      },
      "number": "6010",
      "name": "Agent Johnson"
    },
    "callId": "callhalf-445566778:0",
    "session": {
      "startTime": "2025-03-16T09:00:00Z",
      "stopTime": "2025-03-16T09:15:30Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-03-16T09:00:00Z",
        "mediaStreams": [
          {
            "streamId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "p1-agent-johnson-12345",
            "name": "Agent Johnson",
            "number": "6010",
            "actor": {
              "type": "USER",
              "id": "Y2lzY29zcGFyazovL3VzL1BFT1BMRS9hZ2VudDEyMzQ1Njc4OTBhYmNkZWYxMjM0",
              "email": "agent.johnson@example.com"
            },
            "aor": "sip:agentjohnson@******",
            "send": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "111222333"
              }
            ]
          },
          {
            "id": "p2-pstn-caller-67890",
            "name": "",
            "number": "+14085559999",
            "actor": null,
            "aor": "sip:+14085559999@X.X.X.X;user=phone",
            "send": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "444555666"
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "6010",
          "origCalledNumber": {
            "actor": {
              "type": "CALL_QUEUE",
              "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
            },
            "number": "8000"
          },
          "numOfRedirections": 1
        },
        "acd": {
          "actor": {
            "type": "CALL_QUEUE",
            "id": "Y2lzY29zcGFyazovL3VzL0NBTExfUVVFVUUvYWJjZGVmMTIzNDU2Nzg5MGFiY2Q"
          },
          "acdName": "Customer Support Queue",
          "acdNumber": "8000"
        },
        "announcementData": null
      }
    ]
  }
}
```
