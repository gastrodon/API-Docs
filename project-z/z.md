<details>
<summary>GET /alerts/check</summary>

Check for new activity

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  New activity was fetched

  #### Body
```
{
    "activitiesAlertCount": "int activity alerts",
    "likesAlertCount": "int new likes",
    "followersAlertCount": "int new followers",
    "noticesCount": "int new notices"
}
```


</details>

<details>
<summary>POST /auth/login</summary>

Login to Z with some combination of credentials

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "authType": "int auth type. Password login will be 1, secret or phone login is likely something else",
    "email": "email to this account, if email login",
    "nickname": "user displayed name",
    "password": "password to this account, if a password login",
    "phoneNumber": "phone number to this account, likely if phone login",
    "secret": "valid secret for this account, if a secret login",
    "securityCode": "likely used when a security code is required to login",
    "purpose": "int field or value with an unknown use",
    "birthday": "field or value with an unknown use",
    "contentRegion": "int unknown, appears to be an int representing a region",
    "gender": "the gender of this user",
    "invitationCode": "field or value with an unknown use",
    "school": "field or value with an unknown use"
}
```


#### Responses
- `200`

  The login was ok

  #### Body
```json
{
    "sId": "used to make authorized requests",
    "secret": "likely used to log back in without storing the password",
    "account": {
        "uid": "unique id referencing this resource",
        "status": "int field or value with an unknown use",
        "email": "account email",
        "createdTime": "unix timestamp of occurence",
        "deviceId": "id referencing the clients device",
        "hasProfile": "int does this user have a profile?"
    },
    "userProfile": {
        "uid": "unique id referencing this resource",
        "nickname": "user displayed name",
        "socialId": "unique social id referencing this user",
        "onlineStatus": "int indicator of how this user may be online",
        "nameCardEnabled": "int likely an enum of what name card enabled status is the case for this profile",
        "showsSchool": "int is the profile's school shown?",
        "showsLocation": "int likely bool of whether or not the location of this profile is shown",
        "showsJoinedCircles": "int are joined circles visible?",
        "chatInvitationStatus": "int likely a bool describing whether this user may make chat invites",
        "pushEnabled": "int are push notifs enabled?",
        "gender": "the gender of this user",
        "icon": {
            "baseUrl": "url template to build sizes with",
            "resourceList": [
                {
                    "width": "int width",
                    "height": "int height",
                    "url": "url to the icon in this size",
                    "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                },
                "..."
            ]
        },
        "createdTime": "unix timestamp of occurence",
        "contentRegionName": "name of this profiles region",
        "location": {
            "longitude": "float longitude",
            "latitude": "float latitude",
            "address": {
                "2 character language code": "city location"
            }
        },
        "language": "2 character language code",
        "fansCount": "int number of fans",
        "followingCount": "int number of profiles followed by this profile",
        "friendsCount": "int likely number of people who both are followed by and do follow this profile",
        "socialIdModified": "unique social id referencing this user_modified",
        "status": "int field or value with an unknown use",
        "contentRegion": "int unknown, appears to be an int representing a region",
        "school": "field or value with an unknown use"
    }
}
```


</details>

<details>
<summary>POST /auth/update-push-token</summary>

Update the device push token bound to this account

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "deviceToken": "device token likely used for google push notifications"
}
```


#### Responses
- `200`

  The push token was accepted

  

</details>

<details>
<summary>GET /blogs</summary>

Get a collection of blogs

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of blogs was fetched

  #### Body
```json
{
    "list": [
        {
            "author": {
                "nickname": "user displayed name",
                "uid": "unique id referencing this resource",
                "socialId": "unique social id referencing this user",
                "socialIdModified": "unique social id referencing this user_modified",
                "bio": "information about this user",
                "gender": "the gender of this user",
                "contentRegion": "int unknown, appears to be an int representing a region",
                "contentRegionName": "int unknown, appears to be an int representing a region_name",
                "createdTime": "unix timestamp of occurence",
                "icon": {
                    "baseUrl": "url template to build sizes with",
                    "resourceList": [
                        {
                            "width": "int width",
                            "height": "int height",
                            "url": "url to the icon in this size",
                            "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                        },
                        "..."
                    ]
                },
                "status": "int field or value with an unknown use"
            },
            "blogId": "unique id referencing this resource",
            "uid": "unique id referencing this resource, differnece to blogId is unknown",
            "createdTime": "unix timestamp of occurence",
            "circleIdList": [
                "unique id referencing this resource",
                "..."
            ],
            "content": "blog content",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "language": "2 character language code",
            "mediaList": [
                {
                    "baseUrl": "url template to build sizes with",
                    "resourceList": [
                        {
                            "width": "int width",
                            "height": "int height",
                            "url": "url to the icon in this size",
                            "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                        },
                        "..."
                    ]
                },
                "..."
            ],
            "extensions": "field or value with an unknown use, appears to be an empty object",
            "commentsCount": "int comments",
            "votesCount": "int votes",
            "type": "int field or value with an unknown use, likely blog type",
            "status": "int field or value with an unknown use",
            "visibility": "int field or value with an unknown use"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /chat/joined-threads</summary>

Get a collection of threads that you have joined

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|start|offset this number of items in a collection|No|




#### Responses
- `200`

  A collection of threads was fetched

  #### Body
```json
{
    "isEnd": "bool field or value with an unknown use, probably has to do with pagination",
    "list": [
        {
            "background": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "coHostUids": "probably a list of user ids, but always appears to be null",
            "content": "a description of the chat",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "createdTime": "unix timestamp of occurence",
            "currentMemberInfo": {
                "alertOption": "likely bool int should this chat spawn notifications?",
                "chatMemberStatus": "bool int is the authed profile in this thread?",
                "lastReadMessageId": "unique id referencing this resource",
                "createdTime": "unix timestamp of occurence, likely when the authed profile joined this chat, or epoch if not joined"
            },
            "extensions": "field or value with an unknown use, appears to be an empty object",
            "host": {
                "nickname": "user displayed name",
                "uid": "unique id referencing this resource",
                "socialId": "unique social id referencing this user",
                "socialIdModified": "unique social id referencing this user_modified",
                "bio": "information about this user",
                "gender": "the gender of this user",
                "contentRegion": "int unknown, appears to be an int representing a region",
                "contentRegionName": "int unknown, appears to be an int representing a region_name",
                "createdTime": "unix timestamp of occurence",
                "icon": {
                    "baseUrl": "url template to build sizes with",
                    "resourceList": [
                        {
                            "width": "int width",
                            "height": "int height",
                            "url": "url to the icon in this size",
                            "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                        },
                        "..."
                    ]
                },
                "chatInvitationStatus": "int likely was this user invited to this chat?",
                "chatMemberStatus": "int likely bool is this member a member of this chat?",
                "onlineStatus": "int indicator of how this user may be online",
                "specialTitle": "special title of this user in this chat",
                "status": "int field or value with an unknown use"
            },
            "hostUid": "unique id referencing this resource",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "language": "2 character language code",
            "latestMessage": {
                "author": {
                    "nickname": "user displayed name",
                    "uid": "unique id referencing this resource",
                    "socialId": "unique social id referencing this user",
                    "socialIdModified": "unique social id referencing this user_modified",
                    "bio": "information about this user",
                    "gender": "the gender of this user",
                    "contentRegion": "int unknown, appears to be an int representing a region",
                    "contentRegionName": "int unknown, appears to be an int representing a region_name",
                    "createdTime": "unix timestamp of occurence",
                    "icon": {
                        "baseUrl": "url template to build sizes with",
                        "resourceList": [
                            {
                                "width": "int width",
                                "height": "int height",
                                "url": "url to the icon in this size",
                                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                            },
                            "..."
                        ]
                    },
                    "status": "int field or value with an unknown use"
                },
                "content": "content of the message body",
                "createdTime": "unix timestamp of occurence",
                "messageId": "unique id referencing this resource",
                "threadId": "unique id referencing this resource",
                "uid": "unique id referencing this resource",
                "type": "int type of message"
            },
            "latestMessageId": "unique id referencing this resource",
            "membersCount": "int members in this chat thread",
            "membersSummary": [
                {
                    "nickname": "user displayed name",
                    "uid": "unique id referencing this resource",
                    "socialId": "unique social id referencing this user",
                    "socialIdModified": "unique social id referencing this user_modified",
                    "bio": "information about this user",
                    "gender": "the gender of this user",
                    "contentRegion": "int unknown, appears to be an int representing a region",
                    "contentRegionName": "int unknown, appears to be an int representing a region_name",
                    "createdTime": "unix timestamp of occurence",
                    "icon": {
                        "baseUrl": "url template to build sizes with",
                        "resourceList": [
                            {
                                "width": "int width",
                                "height": "int height",
                                "url": "url to the icon in this size",
                                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                            },
                            "..."
                        ]
                    },
                    "chatInvitationStatus": "int likely was this user invited to this chat?",
                    "chatMemberStatus": "int likely bool is this member a member of this chat?",
                    "onlineStatus": "int indicator of how this user may be online",
                    "specialTitle": "special title of this user in this chat",
                    "status": "int field or value with an unknown use"
                },
                "..."
            ],
            "status": "int field or value with an unknown use",
            "tagList": [
                {
                    "order": "position of this tag, relative to its siblings",
                    "source": "int field or value with an unknown use",
                    "status": "int field or value with an unknown use",
                    "style": {
                        "backgroundColor": "hexidecimal color with alpha bits",
                        "borderColor": "hexidecimal color with alpha bits",
                        "solidColor": "hexidecimal color with alpha bits",
                        "textColor": "hexidecimal color with alpha bits"
                    },
                    "tagId": "int id referencing this tag",
                    "tagName": "name of this tag"
                },
                "..."
            ],
            "threadId": "unique id referencing this resource",
            "title": "title of this chat thread",
            "type": "int field or value with an unknown use"
        },
        "..."
    ],
    "threadCheckList": [
        {
            "threadId": "unique id referencing this resource",
            "latestMessageId": "unique id referencing this resource",
            "lastReadMessageId": "unique id referencing this resource"
        },
        "..."
    ]
}
```


</details>

<details>
<summary>GET /chat/threads</summary>

Get a collection of joinable threads

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of threads was fetched

  #### Body
```json
{
    "list": [
        {
            "background": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "coHostUids": "probably a list of user ids, but always appears to be null",
            "content": "a description of the chat",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "createdTime": "unix timestamp of occurence",
            "currentMemberInfo": {
                "alertOption": "likely bool int should this chat spawn notifications?",
                "chatMemberStatus": "bool int is the authed profile in this thread?",
                "lastReadMessageId": "unique id referencing this resource",
                "createdTime": "unix timestamp of occurence, likely when the authed profile joined this chat, or epoch if not joined"
            },
            "extensions": "field or value with an unknown use, appears to be an empty object",
            "host": {
                "nickname": "user displayed name",
                "uid": "unique id referencing this resource",
                "socialId": "unique social id referencing this user",
                "socialIdModified": "unique social id referencing this user_modified",
                "bio": "information about this user",
                "gender": "the gender of this user",
                "contentRegion": "int unknown, appears to be an int representing a region",
                "contentRegionName": "int unknown, appears to be an int representing a region_name",
                "createdTime": "unix timestamp of occurence",
                "icon": {
                    "baseUrl": "url template to build sizes with",
                    "resourceList": [
                        {
                            "width": "int width",
                            "height": "int height",
                            "url": "url to the icon in this size",
                            "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                        },
                        "..."
                    ]
                },
                "chatInvitationStatus": "int likely was this user invited to this chat?",
                "chatMemberStatus": "int likely bool is this member a member of this chat?",
                "onlineStatus": "int indicator of how this user may be online",
                "specialTitle": "special title of this user in this chat",
                "status": "int field or value with an unknown use"
            },
            "hostUid": "unique id referencing this resource",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "language": "2 character language code",
            "latestMessage": {
                "author": {
                    "nickname": "user displayed name",
                    "uid": "unique id referencing this resource",
                    "socialId": "unique social id referencing this user",
                    "socialIdModified": "unique social id referencing this user_modified",
                    "bio": "information about this user",
                    "gender": "the gender of this user",
                    "contentRegion": "int unknown, appears to be an int representing a region",
                    "contentRegionName": "int unknown, appears to be an int representing a region_name",
                    "createdTime": "unix timestamp of occurence",
                    "icon": {
                        "baseUrl": "url template to build sizes with",
                        "resourceList": [
                            {
                                "width": "int width",
                                "height": "int height",
                                "url": "url to the icon in this size",
                                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                            },
                            "..."
                        ]
                    },
                    "status": "int field or value with an unknown use"
                },
                "content": "content of the message body",
                "createdTime": "unix timestamp of occurence",
                "messageId": "unique id referencing this resource",
                "threadId": "unique id referencing this resource",
                "uid": "unique id referencing this resource",
                "type": "int type of message"
            },
            "latestMessageId": "unique id referencing this resource",
            "membersCount": "int members in this chat thread",
            "membersSummary": [
                {
                    "nickname": "user displayed name",
                    "uid": "unique id referencing this resource",
                    "socialId": "unique social id referencing this user",
                    "socialIdModified": "unique social id referencing this user_modified",
                    "bio": "information about this user",
                    "gender": "the gender of this user",
                    "contentRegion": "int unknown, appears to be an int representing a region",
                    "contentRegionName": "int unknown, appears to be an int representing a region_name",
                    "createdTime": "unix timestamp of occurence",
                    "icon": {
                        "baseUrl": "url template to build sizes with",
                        "resourceList": [
                            {
                                "width": "int width",
                                "height": "int height",
                                "url": "url to the icon in this size",
                                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                            },
                            "..."
                        ]
                    },
                    "chatInvitationStatus": "int likely was this user invited to this chat?",
                    "chatMemberStatus": "int likely bool is this member a member of this chat?",
                    "onlineStatus": "int indicator of how this user may be online",
                    "specialTitle": "special title of this user in this chat",
                    "status": "int field or value with an unknown use"
                },
                "..."
            ],
            "status": "int field or value with an unknown use",
            "tagList": [
                {
                    "order": "position of this tag, relative to its siblings",
                    "source": "int field or value with an unknown use",
                    "status": "int field or value with an unknown use",
                    "style": {
                        "backgroundColor": "hexidecimal color with alpha bits",
                        "borderColor": "hexidecimal color with alpha bits",
                        "solidColor": "hexidecimal color with alpha bits",
                        "textColor": "hexidecimal color with alpha bits"
                    },
                    "tagId": "int id referencing this tag",
                    "tagName": "name of this tag"
                },
                "..."
            ],
            "threadId": "unique id referencing this resource",
            "title": "title of this chat thread",
            "type": "int field or value with an unknown use"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>POST /chat/threads</summary>

Create a new thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "createdTime": "appears to always be 0",
    "hostUid": "appears to always be 0",
    "threadId": "appears to always be 0",
    "uid": "appears to always be 0",
    "title": "title of this thread",
    "type": "int field or value with an unknown use",
    "background": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "latestMessageId": "unique id referencing this resource",
    "status": "int field or value with an unknown use"
}
```


#### Responses
- `200`

  A thread was created

  #### Body
```json
{
    "background": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "coHostUids": "probably a list of user ids, but always appears to be null",
    "content": "a description of the chat",
    "contentRegion": "int unknown, appears to be an int representing a region",
    "createdTime": "unix timestamp of occurence",
    "currentMemberInfo": {
        "alertOption": "likely bool int should this chat spawn notifications?",
        "chatMemberStatus": "bool int is the authed profile in this thread?",
        "lastReadMessageId": "unique id referencing this resource",
        "createdTime": "unix timestamp of occurence, likely when the authed profile joined this chat, or epoch if not joined"
    },
    "extensions": "field or value with an unknown use, appears to be an empty object",
    "host": {
        "nickname": "user displayed name",
        "uid": "unique id referencing this resource",
        "socialId": "unique social id referencing this user",
        "socialIdModified": "unique social id referencing this user_modified",
        "bio": "information about this user",
        "gender": "the gender of this user",
        "contentRegion": "int unknown, appears to be an int representing a region",
        "contentRegionName": "int unknown, appears to be an int representing a region_name",
        "createdTime": "unix timestamp of occurence",
        "icon": {
            "baseUrl": "url template to build sizes with",
            "resourceList": [
                {
                    "width": "int width",
                    "height": "int height",
                    "url": "url to the icon in this size",
                    "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                },
                "..."
            ]
        },
        "chatInvitationStatus": "int likely was this user invited to this chat?",
        "chatMemberStatus": "int likely bool is this member a member of this chat?",
        "onlineStatus": "int indicator of how this user may be online",
        "specialTitle": "special title of this user in this chat",
        "status": "int field or value with an unknown use"
    },
    "hostUid": "unique id referencing this resource",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "language": "2 character language code",
    "latestMessage": {
        "author": {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "status": "int field or value with an unknown use"
        },
        "content": "content of the message body",
        "createdTime": "unix timestamp of occurence",
        "messageId": "unique id referencing this resource",
        "threadId": "unique id referencing this resource",
        "uid": "unique id referencing this resource",
        "type": "int type of message"
    },
    "latestMessageId": "unique id referencing this resource",
    "membersCount": "int members in this chat thread",
    "membersSummary": [
        {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "chatInvitationStatus": "int likely was this user invited to this chat?",
            "chatMemberStatus": "int likely bool is this member a member of this chat?",
            "onlineStatus": "int indicator of how this user may be online",
            "specialTitle": "special title of this user in this chat",
            "status": "int field or value with an unknown use"
        },
        "..."
    ],
    "status": "int field or value with an unknown use",
    "tagList": [
        {
            "order": "position of this tag, relative to its siblings",
            "source": "int field or value with an unknown use",
            "status": "int field or value with an unknown use",
            "style": {
                "backgroundColor": "hexidecimal color with alpha bits",
                "borderColor": "hexidecimal color with alpha bits",
                "solidColor": "hexidecimal color with alpha bits",
                "textColor": "hexidecimal color with alpha bits"
            },
            "tagId": "int id referencing this tag",
            "tagName": "name of this tag"
        },
        "..."
    ],
    "threadId": "unique id referencing this resource",
    "title": "title of this chat thread",
    "type": "int field or value with an unknown use"
}
```


</details>

<details>
<summary>GET /chat/threads/:thread_id</summary>

Get information about some chat thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  Information about this thread was fetched

  #### Body
```json
{
    "background": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "coHostUids": "probably a list of user ids, but always appears to be null",
    "content": "a description of the chat",
    "contentRegion": "int unknown, appears to be an int representing a region",
    "createdTime": "unix timestamp of occurence",
    "currentMemberInfo": {
        "alertOption": "likely bool int should this chat spawn notifications?",
        "chatMemberStatus": "bool int is the authed profile in this thread?",
        "lastReadMessageId": "unique id referencing this resource",
        "createdTime": "unix timestamp of occurence, likely when the authed profile joined this chat, or epoch if not joined"
    },
    "extensions": "field or value with an unknown use, appears to be an empty object",
    "host": {
        "nickname": "user displayed name",
        "uid": "unique id referencing this resource",
        "socialId": "unique social id referencing this user",
        "socialIdModified": "unique social id referencing this user_modified",
        "bio": "information about this user",
        "gender": "the gender of this user",
        "contentRegion": "int unknown, appears to be an int representing a region",
        "contentRegionName": "int unknown, appears to be an int representing a region_name",
        "createdTime": "unix timestamp of occurence",
        "icon": {
            "baseUrl": "url template to build sizes with",
            "resourceList": [
                {
                    "width": "int width",
                    "height": "int height",
                    "url": "url to the icon in this size",
                    "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                },
                "..."
            ]
        },
        "chatInvitationStatus": "int likely was this user invited to this chat?",
        "chatMemberStatus": "int likely bool is this member a member of this chat?",
        "onlineStatus": "int indicator of how this user may be online",
        "specialTitle": "special title of this user in this chat",
        "status": "int field or value with an unknown use"
    },
    "hostUid": "unique id referencing this resource",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "language": "2 character language code",
    "latestMessage": {
        "author": {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "status": "int field or value with an unknown use"
        },
        "content": "content of the message body",
        "createdTime": "unix timestamp of occurence",
        "messageId": "unique id referencing this resource",
        "threadId": "unique id referencing this resource",
        "uid": "unique id referencing this resource",
        "type": "int type of message"
    },
    "latestMessageId": "unique id referencing this resource",
    "membersCount": "int members in this chat thread",
    "membersSummary": [
        {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "chatInvitationStatus": "int likely was this user invited to this chat?",
            "chatMemberStatus": "int likely bool is this member a member of this chat?",
            "onlineStatus": "int indicator of how this user may be online",
            "specialTitle": "special title of this user in this chat",
            "status": "int field or value with an unknown use"
        },
        "..."
    ],
    "status": "int field or value with an unknown use",
    "tagList": [
        {
            "order": "position of this tag, relative to its siblings",
            "source": "int field or value with an unknown use",
            "status": "int field or value with an unknown use",
            "style": {
                "backgroundColor": "hexidecimal color with alpha bits",
                "borderColor": "hexidecimal color with alpha bits",
                "solidColor": "hexidecimal color with alpha bits",
                "textColor": "hexidecimal color with alpha bits"
            },
            "tagId": "int id referencing this tag",
            "tagName": "name of this tag"
        },
        "..."
    ],
    "threadId": "unique id referencing this resource",
    "title": "title of this chat thread",
    "type": "int field or value with an unknown use"
}
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/end-role-play</summary>

End a role play in some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  A role play was ended

  #### Body
```json
{}
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/mark-as-read</summary>

Mark messages in some thread as having been read

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  Chats were marked as read

  #### Body
```json
{}
```


</details>

<details>
<summary>GET /chat/threads/:thread_id/members</summary>

Get a collection of members in some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of members was fetched

  #### Body
```json
{
    "list": [
        {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "chatInvitationStatus": "int likely was this user invited to this chat?",
            "chatMemberStatus": "int likely bool is this member a member of this chat?",
            "onlineStatus": "int indicator of how this user may be online",
            "specialTitle": "special title of this user in this chat",
            "status": "int field or value with an unknown use"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/members</summary>

Join some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  The authed user did join this thread

  #### Body
```json
{}
```


</details>

<details>
<summary>GET /chat/threads/:thread_id/messages</summary>

Get a collection of messages of some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of thread messages was fetched

  #### Body
```json
{
    "list": [
        {
            "author": {
                "nickname": "user displayed name",
                "uid": "unique id referencing this resource",
                "socialId": "unique social id referencing this user",
                "socialIdModified": "unique social id referencing this user_modified",
                "bio": "information about this user",
                "gender": "the gender of this user",
                "contentRegion": "int unknown, appears to be an int representing a region",
                "contentRegionName": "int unknown, appears to be an int representing a region_name",
                "createdTime": "unix timestamp of occurence",
                "icon": {
                    "baseUrl": "url template to build sizes with",
                    "resourceList": [
                        {
                            "width": "int width",
                            "height": "int height",
                            "url": "url to the icon in this size",
                            "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                        },
                        "..."
                    ]
                },
                "chatInvitationStatus": "int likely was this user invited to this chat?",
                "chatMemberStatus": "int likely bool is this member a member of this chat?",
                "onlineStatus": "int indicator of how this user may be online",
                "specialTitle": "special title of this user in this chat",
                "status": "int field or value with an unknown use"
            },
            "messageId": "unique id referencing this resource",
            "threadId": "unique id referencing this resource",
            "uid": "unique id referencing this resource, unknown difference to messageId",
            "asSummary": "show this message as a summary?",
            "content": "body of the message",
            "type": "int likely enum type of message",
            "createdTime": "unix timestamp of occurence"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /chat/threads/:thread_id/online-members</summary>

Get a collection of members online in some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of online members was fetched

  #### Body
```json
{
    "list": [
        {
            "nickname": "user displayed name",
            "uid": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "socialIdModified": "unique social id referencing this user_modified",
            "bio": "information about this user",
            "gender": "the gender of this user",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "contentRegionName": "int unknown, appears to be an int representing a region_name",
            "createdTime": "unix timestamp of occurence",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "chatInvitationStatus": "int likely was this user invited to this chat?",
            "chatMemberStatus": "int likely bool is this member a member of this chat?",
            "onlineStatus": "int indicator of how this user may be online",
            "specialTitle": "special title of this user in this chat",
            "status": "int field or value with an unknown use"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /chat/threads/:thread_id/roles</summary>

Get the roles of some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  A collection of roles was fetched

  #### Body
```json
[
    {
        "roleId": "likely references this role",
        "uid": "uid, unknown difference to roleId",
        "threadId": "uid thread where this role exists",
        "createdTime": "unix timestamp of occurence",
        "name": "name of this role",
        "description": "description of this role",
        "inUse": "is this role in use?",
        "icon": {
            "baseUrl": "url template to build sizes with",
            "resourceList": [
                {
                    "width": "int width",
                    "height": "int height",
                    "url": "url to the icon in this size",
                    "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                },
                "..."
            ]
        },
        "status": "int field or value with an unknown use"
    },
    "..."
]
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/roles</summary>

Create a role in some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "roleId": "likely references this role",
    "uid": "uid, unknown difference to roleId",
    "threadId": "uid thread where this role exists",
    "createdTime": "unix timestamp of occurence",
    "name": "name of this role",
    "description": "description of this role",
    "inUse": "is this role in use?",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "status": "int field or value with an unknown use"
}
```


#### Responses
- `200`

  A role was created

  #### Body
```json
{
    "roleId": "likely references this role",
    "uid": "uid, unknown difference to roleId",
    "threadId": "uid thread where this role exists",
    "createdTime": "unix timestamp of occurence",
    "name": "name of this role",
    "description": "description of this role",
    "inUse": "is this role in use?",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "status": "int field or value with an unknown use"
}
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/roles/:role_id</summary>

Update some role in some thread

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "roleId": "likely references this role",
    "uid": "uid, unknown difference to roleId",
    "threadId": "uid thread where this role exists",
    "createdTime": "unix timestamp of occurence",
    "name": "name of this role",
    "description": "description of this role",
    "inUse": "is this role in use?",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "status": "int field or value with an unknown use"
}
```


#### Responses
- `200`

  A role was modified

  #### Body
```json
{
    "threadId": "thread to create this role in",
    "roleId": "references this role",
    "uid": "unknown difference to roleId",
    "agoraUid": "appears to always be 0",
    "playerUid": "appears to always be 0",
    "roleStatus": "appears to always be 0",
    "name": "name of this role",
    "description": "description of this role",
    "inUse": "is this role in use?",
    "createdTime": "unix timestamp of occurence",
    "status": "int field or value with an unknown use"
}
```


</details>

<details>
<summary>POST /chat/threads/:thread_id/start-role-play</summary>

Start a role play in some thread. Modes are represented as
```
1 -> text
2 -> voice
```

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|


#### Body
```json
{
    "mode": "int role play mode",
    "roleIds": [
        "int role id",
        "..."
    ]
}
```


#### Responses
- `200`

  A role play was started

  #### Body
```json
{}
```


</details>

<details>
<summary>GET /circles</summary>

Get a collection of circles. Currently url param `type` is required, but the API error implies that this is planned to change. Type may be one of `joined`

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|
|type|type of circle to query|Yes|
|uid|query circles joined by the user referenced by this uid|if `type=joined`|




#### Responses
- `200`

  A collection of circles was fetched

  #### Body
```json
{
    "list": [
        {
            "uid": "unique id referencing this resource",
            "circleId": "unique id referencing this resource",
            "socialId": "unique social id referencing this user",
            "name": "name of this circle",
            "tagline": "tagline of this circle",
            "createdTime": "unix timestamp of occurence",
            "status": "int field or value with an unknown use",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "language": "2 character language code",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "tagList": [
                {
                    "order": "position of this tag, relative to its siblings",
                    "source": "int field or value with an unknown use",
                    "status": "int field or value with an unknown use",
                    "style": {
                        "backgroundColor": "hexidecimal color with alpha bits",
                        "borderColor": "hexidecimal color with alpha bits",
                        "solidColor": "hexidecimal color with alpha bits",
                        "textColor": "hexidecimal color with alpha bits"
                    },
                    "tagId": "int id referencing this tag",
                    "tagName": "name of this tag"
                },
                "..."
            ],
            "membersCount": "int number of members"
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /media/default</summary>

Get a collection of default media.
Queried when new chats are created

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|type|type of media to query. Only `1` appears to be valid|Yes|




#### Responses
- `200`

  Default media was fetched

  #### Body
```json
[
    {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "..."
]
```


</details>

<details>
<summary>GET /release-info</summary>

Get information about an app update that may be available

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  Update info was fetched

  #### Body
```json
{
    "Code": "field or value with an unknown use, likely an api status code",
    "Msg": "field or value with an unknown use, likely an api status message",
    "UpdateStatus": "int is the app up to date?",
    "VersionCode": "int target version of the app",
    "VersionName": "semantic version of the app",
    "ModifyContent": "short update changelog",
    "DownloadUrl": "link to the apk containing the target update",
    "ApkSize": "int assumed to be apk size, but is always 0",
    "ApkMd5": "md5 that should be computable from hashing the updated apk"
}
```


</details>

<details>
<summary>GET /tags/suggest</summary>

Get a collection of suggested tags

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|
|word|fetch tags suggested by this word|No|




#### Responses
- `200`

  A collection of suggested tags names was fetcdhed

  #### Body
```json
{
    "list": [
        "tag",
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /users/block-uids</summary>

Get a collection of users who have blocked you, and a collection of users who you have blocked

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  A collection of blocked and blocking users was fetched

  #### Body
```json
{
    "blockedByMeList": [
        "unique id referencing this resource",
        "..."
    ],
    "blockMeList": [
        "unique id referencing this resource",
        "..."
    ]
}
```


</details>

<details>
<summary>GET /users/namecards</summary>

Get a collection of user namecards

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|

###### URL Params
|name|description|required|
| - | - | - |
|size|Return this number of results|No|
|pageToken|Pagination page token|No|




#### Responses
- `200`

  A collection of user namecards was fetched

  #### Body
```json
{
    "list": [
        {
            "uid": "unique id referencing this resource",
            "nickname": "user displayed name",
            "socialId": "unique social id referencing this user",
            "onlineStatus": "int indicator of how this user may be online",
            "nameCardEnabled": "int likely an enum of what name card enabled status is the case for this profile",
            "showsSchool": "int is the profile's school shown?",
            "showsLocation": "int likely bool of whether or not the location of this profile is shown",
            "showsJoinedCircles": "int are joined circles visible?",
            "chatInvitationStatus": "int likely a bool describing whether this user may make chat invites",
            "pushEnabled": "int are push notifs enabled?",
            "gender": "the gender of this user",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            },
            "createdTime": "unix timestamp of occurence",
            "contentRegionName": "name of this profiles region",
            "location": {
                "longitude": "float longitude",
                "latitude": "float latitude",
                "address": {
                    "2 character language code": "city location"
                }
            },
            "language": "2 character language code",
            "fansCount": "int number of fans",
            "followingCount": "int number of profiles followed by this profile",
            "friendsCount": "int likely number of people who both are followed by and do follow this profile",
            "socialIdModified": "unique social id referencing this user_modified",
            "status": "int field or value with an unknown use",
            "contentRegion": "int unknown, appears to be an int representing a region",
            "school": "field or value with an unknown use",
            "taglist": [
                {
                    "order": "position of this tag, relative to its siblings",
                    "source": "int field or value with an unknown use",
                    "status": "int field or value with an unknown use",
                    "style": {
                        "backgroundColor": "hexidecimal color with alpha bits",
                        "borderColor": "hexidecimal color with alpha bits",
                        "solidColor": "hexidecimal color with alpha bits",
                        "textColor": "hexidecimal color with alpha bits"
                    },
                    "tagId": "int id referencing this tag",
                    "tagName": "name of this tag"
                },
                "..."
            ],
            "nameCardBackground": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size",
                        "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
                    },
                    "..."
                ]
            }
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this, if any",
        "total": "int total number of items, if fewer than the size queried"
    }
}
```


</details>

<details>
<summary>GET /users/profile/:user_id</summary>

Get some user profile referenced by a user id

###### Headers
|name|description|required|
| - | - | - |
|rawDeviceId|An id that can identify the device making the request|Yes|
|User-Agent|The user agent of the device making the request|No|
|sId|The authed user's session id|Yes|
|appType|should be `MainApp`|Yes|
|appVersion|the semantic version of this app|Yes|
|deviceType|appears to always be `1`|Yes|
|osType|appears to always be `2`|Yes|




#### Responses
- `200`

  This user was fetched

  #### Body
```json
{
    "uid": "unique id referencing this resource",
    "nickname": "user displayed name",
    "bio": "information about this user",
    "socialId": "unique social id referencing this user",
    "nameCardEnabled": "int likely an enum of what name card enabled status is the case for this profile",
    "showsSchool": "int is the profile's school shown?",
    "showsLocation": "int likely bool of whether or not the location of this profile is shown",
    "showsJoinedCircles": "int are joined circles visible?",
    "chatInvitationStatus": "int likely a bool describing whether this user may make chat invites",
    "pushEnabled": "int are push notifs enabled?",
    "gender": "the gender of this user",
    "icon": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "background": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "nameCardBackground": {
        "baseUrl": "url template to build sizes with",
        "resourceList": [
            {
                "width": "int width",
                "height": "int height",
                "url": "url to the icon in this size",
                "thumbnail": "is this media a thumbnail? Field only appers to be present if its value is true"
            },
            "..."
        ]
    },
    "createdTime": "unix timestamp of occurence",
    "contentRegionName": "name of this profiles region",
    "location": {
        "longitude": "float longitude",
        "latitude": "float latitude",
        "address": {
            "2 character language code": "city location"
        }
    },
    "language": "2 character language code",
    "fansCount": "int number of fans",
    "followingCount": "int number of profiles followed by this profile",
    "friendsCount": "int likely number of people who both are followed by and do follow this profile",
    "onlineStatus": "int indicator of how this user may be online",
    "followMeStatus": "int describing how this user may or may not be following the authed user",
    "followedByMeStatus": "int describing how this user may or may not be followed by the authed user",
    "hasProfile": "int bool does this user have a profile?",
    "socialIdModified": "unique social id referencing this user_modified",
    "status": "int field or value with an unknown use",
    "contentRegion": "int unknown, appears to be an int representing a region",
    "school": "field or value with an unknown use",
    "taglist": [
        {
            "order": "position of this tag, relative to its siblings",
            "source": "int field or value with an unknown use",
            "status": "int field or value with an unknown use",
            "style": {
                "backgroundColor": "hexidecimal color with alpha bits",
                "borderColor": "hexidecimal color with alpha bits",
                "solidColor": "hexidecimal color with alpha bits",
                "textColor": "hexidecimal color with alpha bits"
            },
            "tagId": "int id referencing this tag",
            "tagName": "name of this tag"
        },
        "..."
    ]
}
```


</details>
