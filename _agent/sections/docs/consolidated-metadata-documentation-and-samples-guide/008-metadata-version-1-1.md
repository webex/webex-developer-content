---
type: Excerpt
canonical_url: https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide
lane: production
source_revision: cms-sha256:e1be19c5cbc77e0871ecf36471448c350db9c17483578e472467c7535beb1e5d
publication_state: verified_published_snapshot
heading_hierarchy:
- metadata version 1.1
context_status: requires_parent_review
---

> Documentation excerpt. Cite [the canonical article](https://developer.webex.com/docs/consolidated-metadata-documentation-and-samples-guide). [Full Markdown](../../../../docs/consolidated-metadata-documentation-and-samples-guide.md). Dependencies are not exhaustively verified; read the full article for cross-section procedures or missing context.

## Article introduction

This document describes the various fields of metadata retrieved using the API /v1/convergedRecordings/{recordingId}/metadata for a Webex call recording with a specified recording ID. Additionally, samples of metadata output are provided to explain the metadata for various Webex calling scenarios, such as consult transfer, blind transfer, conference, and call queue features.

---

It covers all the fields associated with call recording metadata. However, it's important to note that many of these fields and pieces of information are not available in the metadata when the query parameter showAllTypes is set to false.

## Selected section

## metadata version 1.1 
#### Scenario: Basic Call. Metadata participants included mediaSessions field with csi information for speaker identification feature.

```json

    "metadata": {
        "version": "1.1",
        "timeStamp": "2024-11-06T13: 50: 30Z",
        "mode": "complete",
        "owner": {
            "type": "USER",
            "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3",
            "name": "dave",
            "orgId": "ee8ebeb0-f077-4384-bb50-9de6141c7bac",
            "locale": "en_US",
            "email": "dave@example.com"
        },
        "storageRegion": "US",
        "locationId": "ed009e16-41f4-47d7-9aa6-c44f687612c0",
        "recordingId": "24af194d-b36b-4829-9d61-7159e9fd1d74",
        "callSessionId": "cf1048d3-3da7-4a15-8590-c1176febdc24",
        "session": {
            "startTime": "2024-11-06T13: 50: 30Z"
        },
        "participants": [
            {
                "id": "c4c63c5d-1826-4101-8849-a4c4f6c23109",
                "aor": "sip: kfb1r1cohm@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "dave", //speaker's name
                "number": "6004",//speaker's number or extension
                "actor": {
                    "type": "USER",
                    "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3",
                    "email": "dave@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "b644ee43-a82d-4819-8666-a17ce337e5f1",
                "aor": "sip: 6001@10.155.4.7;user=phone",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "alice", //speaker's name
                "number": "6001", //speaker's extension
                "actor": {
                    "type": "USER",
                    "id": "efcd7974-9356-4f8d-898f-a784a0a81723",
                    "email": "alice@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 77710816
                    }
                ]
            },
            {
                "id": "1711cd6a-75ab-4656-bb44-5b99550a1117",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "system", // IVR announcement play, speaker name showed as "system"
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "e465a741-ba58-4b1e-877e-b6961e088217",
                "aor": "k6sz63bfwn@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "bob",
                "number": "6002",
                "actor": {
                    "type": "USER",
                    "id": "6bb0b081-591f-472e-9b4e-afab20089c6b",
                    "email": "bob@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 706733971
                    }
                ]
            },
            {
                "id": "308de675-5ca2-465f-9996-923e9474b1c4",
                "aor": "gz8ilbortg@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "carol",
                "number": "6003",
                "actor": {
                    "type": "USER",
                    "id": "0a9b1a7e-2063-4d77-a7da-ffb396b0d389",
                    "email": "carol@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 
                    }
                ]
            },
            {
                "id": "85c18827-fa97-4990-98ba-af74f3674ef7",
                "aor": "izqyme3qip@64941297.int10.bcld.webex.com",
                "send": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "name": "emily",
                "number": "6005",
                "actor": {
                    "type": "USER",
                    "id": "9650d89e-f0bd-4117-86e4-efce06fea374",
                    "email": "emily@example.com"
                },
                "mediaSessions": [
                    {
                        "mediaType": "audio",
                        "mediaContent": "main",
                        "csi": 221319636
                    }
                ]
            }
        ],
        "mediaStreams": [
            {
                "streamId": "e6975b6d-3a14-498b-a000-22d6201fd461",
                "mode": "mixed",
                "mLineIndex": "0"
            }
        ],
        "extensionData": {
            "recordingType": "alwaysON",
            "userId": "kfb1r1cohm@64941297.int10.bcld.webex.com",
            "callId": "callhalf-101170306: 0",
            "callData": {
                "type": "origCall",
                "callingParty": {
                    "actor": {
                        "type": "USER",
                        "id": "1c3cf09a-560a-44c4-8fc6-00df4d4bdcc3"
                    },
                    "number": "6004",
                    "name": "dave"
                },
                "calledParty": {
                    "actor": {
                        "type": "USER",
                        "id": "efcd7974-9356-4f8d-898f-a784a0a81723"
                    },
                    "number": "6001",
                    "name": "alice"
                },
                "dialedDigits": "sip: 6001@10.155.4.7"
            }
        }
    }
```

#### Scenario: Outgoing PSTN call. Metadata participants included mediaSessions field with csi information for speaker identification feature.

```json

 {
  "id": "029cf270-13f6-46ab-ba31-37dc810aa0b2",
  "orgId": "9b766f58-6cfc-473a-871e-a55459829cde",
  "ownerId": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
  "ownerType": "USER",
  "ownerName": "carol",
  "ownerEmail": "carol@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "029cf270-13f6-46ab-ba31-37dc810aa0b2",
    "locationId": "4907ed26-0fb4-47ce-be9d-4e1ac3ce1afb",
    "callSessionId": "795c5ef8-f871-48e7-afcb-842007281226",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
        "email": null
      },
      "number": "",
      "name": "carol"
    },
    "calledParty": {
      "actor": null,
      "number": "",
      "name": ""
    },
    "callId": "callhalf-109517238:0",
    "session": {
      "startTime": "2024-11-27T07:55:49Z",
      "stopTime": null
    },
    "recordingType": "alwaysON",
    "answererInfo": null,
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2024-11-27T07:55:49Z",
        "mediaStreams": [
          {
            "streamId": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "a41de2bc-abde-4b7e-a0af-7c19c79a7cd6",
            "name": "carol",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "12693e0b-e82f-4f3b-9e3a-4b918b6d2694",
              "email": "carol@example.com"
            },
            "aor": "sip:dcrvlqxti7@******",
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
          },
          {
            "id": "4d64c490-d40b-4aca-856f-9e5cf8ab196e",
            "name": "",
            "number": "",
            "actor": null,
            "aor": "sip:@X.X.X.X;user=phone",
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
          },
          {
            "id": "494a6b6a-40ee-4842-83c7-d2be02d5a649",
            "name": "system",
            "number": null,
            "actor": null,
            "aor": null,
            "send": "bde0a38e-0d42-44a2-b930-a5d5b6860dbf",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "",
                "previousCsis": null
              }
            ]
          }
        ],
        "redirectInfo": null,
        "redirectedCall": null,
        "acd": null,
        "announcementData": null
      }
    ]
  }
}
```

#### Scenario: Call hold-resume

```json
{
  "id": "436ba427-2ea2-46ab-9e0c-f6c156189bf0",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "IN",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "436ba427-2ea2-46ab-9e0c-f6c156189bf0",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "ed9ae7c9-5cc1-4e44-9384-fa4c8ccf699c",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
      },
      "number": "8001",
      "name": "bob"
    },
    "callId": "callhalf-73322436:0",
    "session": {
      "startTime": "2025-01-09T02:43:00Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:43:00Z",
        "mediaStreams": [
          {
            "streamId": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "1a62c69a-87ab-4e49-a999-429a5fde5c05",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "225001639"
              }
            ]
          },
          {
            "id": "f4a23718-a02b-49cf-8c50-4032f6888c63",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "sip:8001@X.X.X.X;user=phone",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "9895bcee-c89e-4e44-9347-12a4cee6ab8e",
            "name": "system",
            "send": "264909ee-0c26-4fc5-9c9c-b907d043bf0d",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ]
      }
    ]
  }
}
```

#### Scenario: Blind call transfer

```json


{
  "id": "f53e4f4b-122c-41e5-82f2-907b18ecec4b",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
  "ownerType": "USER",
  "ownerName": ". carol",
  "ownerEmail": "carol@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "f53e4f4b-122c-41e5-82f2-907b18ecec4b",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "61afe5ef-3d3e-477f-86a0-4584fc81775d",
    "personality": "terminator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "8000",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2"
      },
      "number": "7002",
      "name": "carol"
    },
    "callId": "callhalf-73323092:0",
    "session": {
      "startTime": "2025-01-09T02:44:27Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:44:27Z",
        "mediaStreams": [
          {
            "streamId": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "4abf7d1b-9fa3-4334-a281-1b5ee8600e5e",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:o5o1guuv31@******",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "f306ac2b-4629-4336-9f04-ce2058d76650",
            "name": "alice",
            "number": "8000",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:8000@X.X.X.X;user=phone",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "c919c3a6-86f2-4a17-b37240",
            "name": "system",
            "send": "8de303d5-77fd-4f1d-b94e-ad5bb17b0c87",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ],
        "redirectInfo": {
          "lastRedirectNumber": "7002",
          "origCalledNumber": {
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
            },
            "number": ""
          },
          "numOfRedirections": 1
        }
      }
    ]
  }
}
```

#### Scenario: Consult call transfer

```json

{
  "id": "ec7315eb-f5a7-4c49-be0d-f510ead3212b",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "ec7315eb-f5a7-4c49-be0d-f510ead3212b",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "61afe5ef-3d3e-477f-86a0-4584fc81775d",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a"
      },
      "number": "8001",
      "name": "bob"
    },
    "callId": "callhalf-73322940:0",
    "session": {
      "startTime": "2025-01-09T02:44:06Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:44:06Z",
        "mediaStreams": [
          {
            "streamId": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "bc631506-a93d-4fb3-a420-74df70cff9a0",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": "727981502"
              }
            ]
          },
          {
            "id": "4d1671e2-bcd9-4ade-9a3b-2b151db431ed",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "sip:8001@X.X.X.X;user=phone",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "bbf1e699-454a-469f-b1f8-b9d164b45b25",
            "name": "system",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "ea95a2d2-7c44-4f5e-bc6f-5c024e541ccd",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone"
          },
          {
            "id": "82e4d767-f117-4823-9933-16d8fa473365",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone",
            "send": "5b3c5b46-7bc0-43e3-af56-e4f2d5affe50",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ],
        "redirectedCall": {
          "redirectedFromPartyNumber": "8001",
          "redirectedToPartyNumber": "sip:7002@X.X.X.X;user=phone"
        }
      }
    ]
  }
}
```
#### Scenario: Conference call

```json
{
  "id": "726bbaef-321c-4a41-8ec8-36d901a09f49",
  "orgId": "58a83156-5c62-4453-a852-ecf688935e5c",
  "ownerId": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
  "ownerType": "USER",
  "ownerName": ". alice",
  "ownerEmail": "alice@example.com",
  "storageRegion": "US",
  "serviceType": "calling",
  "version": "1.1",
  "serviceData": {
    "callRecordingId": "726bbaef-321c-4a41-8ec8-36d901a09f49",
    "locationId": "06ea4b8a-2250-4a57-8f13-43d0dd8d3616",
    "callSessionId": "55e45a6c-d42b-4bb7-87f1-0808f4a66156",
    "personality": "originator",
    "callingParty": {
      "actor": {
        "type": "USER",
        "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b"
      },
      "number": "",
      "name": "alice"
    },
    "calledParty": {
      "actor": {
        "type": "USER",
        "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2"
      },
      "number": "7002",
      "name": "carol"
    },
    "callId": "callhalf-73323568:1",
    "session": {
      "startTime": "2025-01-09T02:45:51Z"
    },
    "recordingType": "alwaysON",
    "recordingActions": [],
    "callActivity": [
      {
        "timeStamp": "2025-01-09T02:45:51Z",
        "mediaStreams": [
          {
            "streamId": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mode": "mixed",
            "mLineIndex": "0"
          }
        ],
        "participants": [
          {
            "id": "4110698b-3267-46d6-b6eb-7177a0ecd07e",
            "name": "alice",
            "number": "",
            "actor": {
              "type": "USER",
              "id": "069e9104-e33b-4a4c-bc3a-6dcd12c3904b",
              "email": "alice@example.com"
            },
            "aor": "sip:d02nnt2aor@******",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "2f6e4899-29a2-4a2c-8f58-ee0c24dd63e9",
            "name": "carol",
            "number": "7002",
            "actor": {
              "type": "USER",
              "id": "42aed5d9-9c47-4387-b51a-e7fa16ae95f2",
              "email": "carol@example.com"
            },
            "aor": "sip:7002@X.X.X.X;user=phone",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "0914ed1f-45a9-49f8-8c70-effe271a0e15",
            "name": "system",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          },
          {
            "id": "a8224e4e-3583-4a36-a7f1-f9db8e042f1f",
            "name": "bob",
            "number": "8001",
            "actor": {
              "type": "USER",
              "id": "1efc4159-48a2-4244-ba04-37bc8e4f6c1a",
              "email": "bob@example.com"
            },
            "aor": "wgqwgarksy@******",
            "send": "c54f5c00-793e-4165-9d50-f324d4cdc030",
            "mediaSessions": [
              {
                "mediaType": "audio",
                "mediaContent": "main",
                "csi": ""
              }
            ]
          }
        ]
      }
    ]
  }
}
```
