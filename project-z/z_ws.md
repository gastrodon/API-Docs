<details>
<summary>SEND enter-thread</summary>

Enter a thread and start recieving websocket updates for its events



#### Body
```json
{
    "t": 6,
    "threadId": "referencing the thread to enter"
}
```



</details>

<details>
<summary>SEND message</summary>

Send a chat message



#### Body
```json
{
    "t": 1,
    "msg": {
        "applyCount": "likely appears to always be 0",
        "asSummary": "field or value with an unknown use",
        "content": "thread message content",
        "createdTime": "appears to always be 0",
        "extensions": {
            "contentStatus": "field or value with an unknown use",
            "friendshipLevel": "field or value with an unknown use"
        },
        "memberList": [
            "likely members who are online or recipient",
            "..."
        ],
        "messageId": "likely appears to always be 0",
        "refId": "int likely unique socket message id",
        "roleList": [
            "likely roles applying to sender or recipient",
            "..."
        ],
        "rolePlayMode": "int likely bool was this sent as part of a role play?",
        "status": "int field or value with an unknown use",
        "threadActivityType": "field or value with an unknown use",
        "threadId": "referencing thread to send this message to",
        "type": "int likely type of message sent",
        "uid": "referencing something unknown",
        "userList": [
            "unknown, likely uid referencing users",
            "..."
        ]
    },
    "threadId": "appears to be same as msg.threadId"
}
```



</details>

<details>
<summary>RECV ping</summary>

The server is sending a ping






</details>

<details>
<summary>SEND pong</summary>

Send a resposne to a Ping






</details>

<details>
<summary>RECV system-role-play-start</summary>

A system message stating that a role play has started



#### Body
```json
{
    "msg": {
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
        "createdTime": "unix timestamp of occurence",
        "messageId": 0,
        "threadId": "referencing the thread this is in",
        "type": "43, likely represents a role play start",
        "uid": "referencing unknown"
    },
    "t": 1
}
```



</details>
