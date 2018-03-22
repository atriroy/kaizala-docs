# Schema details of Webhook response for registered events

If a webhook is registered, Kaizala returns a webHook response for each event on the registered objectId, filtered for registered events. 
Below is schema details for different webhook response for different events.

## Response Body
| Parameter | Type | Description |
| :---: | :---: | :--- |
| objectId | String | Identifier representing the object in which context the webhook has been created.For ObjectType=Group, its group's Identifier, For ObjectType=Action, its actionId, For ObjectType=ActionPackage, its action-package-id |
| objectType | String | Enum: "Group"/"Action"/"ActionPackage" |
| eventType | String | Registered event that has been invoked |
| eventId | String | Identifier representing the event |
| data | JSON Object | Object representing data specific to that event. Parameters defined below for each of the supported event. |
| context | String | Returns value that has been set while registering a webhook under parameter 'callbackContext'|
| fromUser | String | Sender's phone number |
| fromUserId | String | Sender's userId |
| fromUserName | String | Sender's registered name with Kaizala |
| fromUserProfilePic | url | Sender's Profile Pic |

### data for event 'TextMessageCreated'
| Parameter | Type | Description |
| :---: | :---: | :--- |
| text | String | Text Message that has been sent |

#### Sample webHook response for 'TextMessageCreated'
```javascript
{
  "objectId": "8c2050-9be8-45d6-97f5-bb7013930027",
  "objectType": "Group",
  "eventType": "TextMessageCreated",
  "eventId": "55ed01-02b5-491e-8e7e-484726da976b",
  "data": {
    "text": "Test Message"
  },
  "context": "Any data which is required to be returned in callback",
  "fromUser": "+91xxxxxxxx",
  "fromUserId": "72e91-f3-4e7b-84eb-4e228406fb9b",
  "isBotfromUser": false,
  "fromUserName": "Robin Richard",
  "fromUserProfilePic": "https://mobileonlyapps.blob.core.windows.net/72e29591-4e7b-84eb-4e228406fb9b/c34afc0d53614ae29285d08e6409e416.jpg"
}
```

### data for event 'AttachmentCreated'
| Parameter | Type | Description |
| :---: | :---: | :--- |
| media | Array | Each item contains mediaUrl and mediaFileName|
| mediaUrl | url | url of the image |
| mediaFileName | String | Filename |
| actionType | String | Enum value : 'Image' |
| caption | String | caption attached with the image |

#### Sample webHook response for 'AttachmentCreated'
```javascript
{
  "objectId": "8c291050-9be8-45d6-97f5-bb7013930027",
  "objectType": "Group",
  "eventType": "AttachmentCreated",
  "eventId": "59e2e9f9-9b10-4b67-8bc5-3f85a04f2d91",
  "data": {
    "media": [
      {
        "mediaUrl": "https://cdn.inc-000.kms.osi.office.net/att/0ad142c52b30d797addebadb620c19bf6f018299ed4acdce5760e45e2e4bc4ae.jpg?sv=2015-12-11&amp;sr=b&amp;sig=Thbp46wdgoqbDaAF06v2Y2ijzny0jx2fBDo1EZab%2BNY%3D&amp;st=2018-03-22T10:22:21Z&amp;se=2292-01-05T11:22:21Z&amp;sp=r",
        "mediaFileName": "IMG_18-03-22_165220084_1.jpg"
      }
    ],
    "actionType": "Image",
    "caption": "Testing."
  },
 "context": "Any data which is required to be returned in callback",
  "fromUser": "+91xxxxxxxx",
  "fromUserId": "72e91-f3-4e7b-84eb-4e228406fb9b",
  "isBotfromUser": false,
  "fromUserName": "Robin Richard",
  "fromUserProfilePic": "https://mobileonlyapps.blob.core.windows.net/72e29591-4e7b-84eb-4e228406fb9b/c34afc0d53614ae29285d08e6409e416.jpg"
}
```
### data for event 'Announcement'
| Parameter | Type | Description |
| :---: | :---: | :--- |
| title | String | Title of Announcement Action |
| text | String | Message body of Announcement Action |
| media | Array | Each item contains mediaUrl and mediaFileName|
| mediaUrl | url | url of the image |
| mediaFileName | String | Filename |


#### Sample webHook response for 'Announcement'
```javascript
{
  "objectId": "8c291050-9be8-45d6-97f5-bb7013930027",
  "objectType": "Group",
  "eventType": "Announcement",
  "eventId": "3e49b367-acf6-48a7-a675-6bf4d372a070",
  "data": {
    "text": "Caption :Testing.",
    "title": "Sent by Nitin Jaiswal",
    "media": [
      {
        "url": "https://cdn.inc-000.kms.osi.office.net/contenthost/beb2cfef8732c6cc3b54652c1f6f99d64f529fd9be3d409e2966552639fb791f.jpeg",
        "fileName": "e3c145f1-5e6f-4ee9-bd83-49ec3a1c2550.jpeg"
      }
    ]
  },
 "context": "Any data which is required to be returned in callback",
  "fromUser": "+91xxxxxxxx",
  "fromUserId": "72e91-f3-4e7b-84eb-4e228406fb9b",
  "isBotfromUser": false,
  "fromUserName": "Robin Richard",
  "fromUserProfilePic": "https://mobileonlyapps.blob.core.windows.net/72e29591-4e7b-84eb-4e228406fb9b/c34afc0d53614ae29285d08e6409e416.jpg"
}
```

### data for event 'JobCreated'
| Parameter | Type | Description |
| :---: | :---: | :--- |
| title | String | Title of Announcement Action |
| text | String | Message body of Announcement Action |
| actionId | Id | Identifier for that particular instance of Job Action |
| dueDate | Date | Date by which job would expire |
| assignedTo | String Array | Array of phone numbers |


#### Sample webHook response for 'JobCreated'
```javascript
{
  "objectId": "8c2950-9be8-45d6-97f5-bb7013930027",
  "objectType": "Group",
  "eventType": "JobCreated",
  "eventId": "3e49b367-acf6-48a7-a675-6bf4d372a070",
  "data": {
    "assignedTo": [
      "+919740797266"
    ],
    "title": "Test Job",
    "dueDate": "2018-03-22T18:29:59Z",
    "actionId": "aeb012-31a0-477a-a131-8a1e2791b36e",
    "groupId": "8c291050-9be8-6-97f5-bb7013930027"
  },
 "context": "Any data which is required to be returned in callback",
  "fromUser": "+91xxxxxxxx",
  "fromUserId": "72e91-f3-4e7b-84eb-4e228406fb9b",
  "isBotfromUser": false,
  "fromUserName": "Robin Richard",
  "fromUserProfilePic": "https://mobileonlyapps.blob.core.windows.net/72e29591-4e7b-84eb-4e228406fb9b/c34afc0d53614ae29285d08e6409e416.jpg"
}
```
