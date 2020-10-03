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
    "birthday": "field or value with an unknown use",
    "contentRegion": " int field or value with an unknown use",
    "email": "email to this account, if email login",
    "gender": "int field or value with an unknown use",
    "invitationCode": "field or value with an unknown use",
    "nickname": "nickname to this account, likely if nickname login",
    "password": "password to this account, if a password login",
    "phoneNumber": "phone number to this account, likely if phone login",
    "purpose": "int field or value with an unknown use",
    "school": "field or value with an unknown use",
    "secret": "valid secret for this account, if a secret login",
    "securityCode": "likely used when a security code is required to login"
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
        "uid": "unique id referencing this user",
        "status": "int field or value with an unknown use",
        "email": "account email",
        "createdTime": "unix timestamp of occurence",
        "deviceId": "id referencing the clients device",
        "hasProfile": "int does this user have a profile?"
    },
    "userProfile": {
        "uid": "unique id referencing this user",
        "nickname": "profile nickname",
        "socialId": "profile social id",
        "onlineStatus": "int field or value with an unknown use, but related to whether or not the profile is online",
        "nameCardEnabled": "int likely an enum of what name card enabled status is the case for this profile",
        "showsSchool": "int is the profile's school shown?",
        "showsLocation": "int likely bool of whether or not the location of this profile is shown",
        "showsJoinedCircles": "int are joined circles visible?",
        "chatInvitationStatus": "int likely a bool describing whether this user may make chat invites",
        "pushEnabled": "int are push notifs enabled?",
        "gender": "int likely a gender bool",
        "icon": {
            "baseUrl": "url template to build sizes with",
            "resourceList": [
                {
                    "width": "int width",
                    "height": "int height",
                    "url": "url to the icon in this size"
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
        "socialIdModified": "int field or value with an unknown use",
        "status": "field or value with an unknown use",
        "contentRegion": "int field or value with an unknown use",
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
            "uid": "unique id referencing this user",
            "nickname": "profile nickname",
            "socialId": "profile social id",
            "onlineStatus": "int field or value with an unknown use, but related to whether or not the profile is online",
            "nameCardEnabled": "int likely an enum of what name card enabled status is the case for this profile",
            "showsSchool": "int is the profile's school shown?",
            "showsLocation": "int likely bool of whether or not the location of this profile is shown",
            "showsJoinedCircles": "int are joined circles visible?",
            "chatInvitationStatus": "int likely a bool describing whether this user may make chat invites",
            "pushEnabled": "int are push notifs enabled?",
            "gender": "int likely a gender bool",
            "icon": {
                "baseUrl": "url template to build sizes with",
                "resourceList": [
                    {
                        "width": "int width",
                        "height": "int height",
                        "url": "url to the icon in this size"
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
            "socialIdModified": "int field or value with an unknown use",
            "status": "field or value with an unknown use",
            "contentRegion": "int field or value with an unknown use",
            "school": "field or value with an unknown use",
            "taglist": [
                {
                    "order": "position of this tag, relative to its siblings",
                    "source": "int field or value with an unknown use",
                    "status": "int field or value with an unknown use",
                    "style": {
                        "backgroundColor": "$data.string.alpha_color",
                        "borderColor": "$data.string.alpha_color",
                        "solidColor": "$data.string.alpha_color",
                        "textColor": "$data.string.alpha_color"
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
                        "url": "url to the icon in this size"
                    },
                    "..."
                ]
            }
        },
        "..."
    ],
    "pagination": {
        "nextPageToken": "token to fetch the next page relative to this"
    }
}
```


</details>
