<details>
<summary>GET /account/id/:id</summary>
Get a user by their id

__url params__

|name|description|
| - | - |
|id|the id of the user to query|

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - User information recieved
User information recieved

A user of id `id` exists and was retrieved

```JSON
{
    "data": {
        "avatarURL": "...                   <Account pfp link>",
        "backgroundColor": "#000000         <Account background color",
        "bio": "...                         <Account bio>",
        "displayName": "...                 <Non-unique display name>",
        "followerCount": "0                 <Subscribers of this account>",
        "followingCount": "0                <Subscriptions of this account>",
        "foregroundColor": "#CCD6E9         <Account foreground color",
        "id": "                             <Account id>",
        "isBlocked": "false                 <Is this user blocked by the authed user?>",
        "isChannel": "false                 <Is this user a channel?>",
        "isFollowed": "false                <Is this user being followed by the authed user?>",
        "isFollowing": "false               <Is this user following the authed user?>",
        "loopCount": "0                     <Total loops played of this account>",
        "loopsConsumedCount": "0            <Total loops played by this account>",
        "registrationDate": "1580272854     <Account creation Unix timestamp>",
        "username": "robotter               <Account username>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /account/id/:id/posts</summary>
Get posts by some user

__url params__

|name|description|
| - | - |
|id|the id of the user to query|

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /account/id/:id/rebytes</summary>
Get rebytes by some user

__url params__

|name|description|
| - | - |
|id|the id of the user to query|

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "rebytes": "[...]   <Array of post rebytes>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /account/me</summary>
Get information about the logged in account

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Account fetched
Account fetched

The account information of the logged in user was fetched

```JSON
{
    "data": {
        "account": {
            "backgroundColor": "#000000         <Account background color",
            "followerCount": "0                 <Subscribers of this account>",
            "followingCount": "0                <Subscriptions of this account>",
            "foregroundColor": "#CCD6E9         <Account foreground color",
            "id": "                             <account id>",
            "isChannel": "false                 <Is this user a channel?>",
            "isDeactivated": "false             <Did this user deactivate their account?>",
            "isRegistered": "true               <Is this user registered?>",
            "isSuspended": "false               <Is this account suspended?>",
            "loopCount": "0                     <Total loops played of this account>",
            "loopsConsumedCount": "0            <Total loops played by this account>",
            "registrationDate": "1580272854     <Account creation Unix timestamp>",
            "username": "robotter               <Account username>"
        }
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>
<details>
<summary>PUT /account/me</summary>
Update the authed user.
Any or all of the json fields may be included or omitted,
but the request will only work if all data being sent is new


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

```JSON
{
    "colorScheme": "2       <Predefined color scheme to use>",
    "bio": "...             <Profile bio to use, send a blank to remove>",
    "displayName": "...     <Non-unique display name to use, send blank to remove>",
    "username": "...        <Unique username to use>"
}
```

__responses__

- 200 - Account updated
Account updated

The information sent was ok and the profile information is updated

```JSON
{
    "data": {},
    "success": 1
}
```

- 200:1101 - Bad request format
Bad request format

The information sent is either malformed, has missing keys, or has unexpected extra keys.
It cannot be used. This should be treated similarly too an HTTP 400 bad request


```JSON
{
    "error": {
        "code": 1101,
        "message": "bad request format"
    },
    "success": 0
}
```

- 200:1401 - Username invalid
Username invalid

The username sent is too long or has bad characters

```JSON
{
    "success": 0,
    "error": {
        "code": 1401,
        "message": "invalid username"
    }
}
```

- 200:1402 - Username taken
Username taken

The username sent is already taken and cannot be used

```JSON
{
    "success": 0,
    "error": {
        "code": 1402,
        "message": "username is already in use"
    }
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>PUT /account/me/device</summary>
Give byte information about this device

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

```JSON
{
    "applicationID": "co.byte  <Seems to accept arbitrary strings>",
    "deviceToken": "...        <Device token. Appears to be generated by the app, seems to accept an arbitrary string>",
    "deviceType": "android     <Only android seems to work. iOS / Apple string unknown>"
}
```

__responses__

- 200 - Device info accepted
Device info accepted

The device info sent is correct and was accepted

```JSON
{
    "data": {},
    "success": 1
}
```

- 200:1101 - Bad request format
Bad request format

The information sent is either malformed, has missing keys, or has unexpected extra keys.
It cannot be used. This should be treated similarly too an HTTP 400 bad request


```JSON
{
    "error": {
        "code": 1101,
        "message": "bad request format"
    },
    "success": 0
}
```

- 200:1404 - Device info incorrect
Device info incorrect

The device info sent is malformed

```JSON
{
    "error": {
        "code": 1404,
        "message": "invalid device type"
    },
    "success": 0
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /account/prefix/:prefix</summary>
Search for users by some username `prefix`

__url params__

|name|description|
| - | - |
|prefix|prefix to search for|

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Search results fetched
Search results fetched

Search results for the prefix used were returned

```JSON
{
    "data": {
        "accounts": [
            {
                "avatarURL": "...                   <Account pfp link>",
                "backgroundColor": "#000000         <Account background color",
                "bio": "...                         <Account bio>",
                "displayName": "...                 <Non-unique display name>",
                "followerCount": "0                 <Subscribers of this account>",
                "followingCount": "0                <Subscriptions of this account>",
                "foregroundColor": "#CCD6E9         <Account foreground color",
                "id": "                             <Account id>",
                "isBlocked": "false                 <Is this user blocked by the authed user?>",
                "isChannel": "false                 <Is this user a channel?>",
                "isFollowed": "false                <Is this user being followed by the authed user?>",
                "isFollowing": "false               <Is this user following the authed user?>",
                "loopCount": "0                     <Total loops played of this account>",
                "loopsConsumedCount": "0            <Total loops played by this account>",
                "registrationDate": "1580272854     <Account creation Unix timestamp>",
                "username": "robotter               <Account username>"
            }
        ]
    },
    "success": 1
}
```

- 200:1401 - Bad search
Bad search

Search string has invalid characters that cannot prefix a username

```JSON
{
    "success": 0,
    "error": {
        "code": 1401,
        "message": "invalid username"
    }
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /categories</summary>
Get a list of feed categories. These can be used in the /feed/categories/:id endpoint

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Categories fetched
Categories fetched

A list of categories has been fetched

```JSON
{
    "data": {
        "categories": [
            {
                "icon": "...    <Category icon link. This is usually 200px",
                "id": "comedy   <Category id, used in /feed/categories/:id>",
                "name": "Comedy <Category name>"
            }
        ]
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>POST /client/event</summary>
Likely has to do with event tracking. Appears to always ratelimit me

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Event accepted
Event accepted

The recorded event was accepted and recorded

```JSON
{
    "data": {},
    "success": 1
}
```

- 200:1101 - Bad request format
Bad request format

The information sent is either malformed, has missing keys, or has unexpected extra keys.
It cannot be used. This should be treated similarly too an HTTP 400 bad request


```JSON
{
    "error": {
        "code": 1101,
        "message": "bad request format"
    },
    "success": 0
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /explore</summary>
Get possible explore feeds

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Explore cards recieved
Explore cards recieved

The current explore cards have been fetched

```JSON
{
    "data": {
        "layout": [
            {
                "background": {
                    "color": "#00BBDB           <Card background color>",
                    "type": "image              <Card background type>",
                    "url": "...                 <Background image link, if any such background>"
                },
                "description": "null            <Card description, if any>",
                "header": {
                    "backgroundColor": "null    <Header background color>",
                    "color": "null              <Header color>",
                    "title": "Popular Now       <Header title>"
                },
                "icon": "null                   <Icon link, if any such icon>",
                "sponsored": "false             <Is this sponsored? Ads appear to not yet be implemented>",
                "title": {
                    "backgroundColor": "null    <Appears to always be nil>",
                    "color": "#ffffff           <Title color>",
                    "title": "Popular Now       <Title title>"
                },
                "type": "large                  <Card display type, observed include [image, large, medium]",
                "uri": "byte://...              <Byte-handleable endpoint. byte:// can be subbed for the api's baseurl>"
            }
        ]
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /feed/categories/:id/popular</summary>
Get a slice of popular posts in some category, denoted by its id.
The only observed sub-endpoint for any category is `popular`.
Lists of categories can be fetched with GET `/categories`


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /feed/global</summary>
Get data from the global feed

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /feed/mix</summary>
Get a slice of posts in the mix feed.
This seems to be a mixed feed of posts, possibly comparable to ifunny/collective


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /feed/popular/v2</summary>
Get a slice of posts in the popular feed.
These posts are mostly based on raw popularity, with little to no algorithmic influence.
This is different than the /v3/ endpoint, which is an algorithm based feed for some user


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /feed/popular/v3</summary>
Get a slice of posts in the popular:v3 feed.
These posts are curated by an algorithm, not necessarially popular.
For regular popular, see the /v2/ endpoint, which is mostly purely popular


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /post/id/:id</summary>
Get a post by its id

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Post retrieved
Post retrieved

A post of id `id` exists and was retrieved

```JSON
{
    "data": {
        "accounts": "{...}      <id -> profile map>",
        "allowCuration": "true  <May this post be curated?>",
        "allowRemix": "false    <May this post be remixed?>",
        "authorID": "...        <Post author id>",
        "caption": "...         <Post caption>",
        "commentCount": "6633   <Total comment count>",
        "commentCursor": "...   <Comments paging cursor>",
        "comments": "[...]      <Array of comments>",
        "date": "1579934060     <Post create timestamp>",
        "id": "...              <Post id>",
        "likeCount": "119453    <Total like count>",
        "likedByMe": "false     <Did the authed user like this post?>",
        "loopCount": "2356580   <Total loop count>",
        "mentions": "[]         <Array of mentions>",
        "rebytedByMe": "false   <Did the authed user rebyte this post?>",
        "thumbSrc": "...        <Thumbnail resource link>",
        "type": "0              <Unknown>",
        "videoSrc": "...        <Video resource link>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /post/id/:id/feedback/comments</summary>
Get a slice of comments on a post with usermap data

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Comment slice recieved
Comment slice recieved

A slice of comments was fetched

```JSON
{
    "data": {
        "accounts": "{...}                  <id -> profile map>",
        "comments": [
            {
                "authorID": "...            <Comment author id>",
                "body": "...                <Comment text body>",
                "date": "1580275243         <Comment create timestamp>",
                "id": "...-...              <Comment id as <post_id>-<comment_id>",
                "mentions": [
                    {
                        "accountID": "...   <Account mentioned>",
                        "byteRange": {
                            "start": "10    <Unknown>",
                            "stop": "15     <Unknown, same length as range>"
                        },
                        "range": {
                            "start": "8     <Mention substring start>",
                            "stop": "13     <Mention substring end>"
                        },
                        "text": "@byte      <Mention text>",
                        "username": "byte   <Username mentioned"
                    }
                ],
                "postID": "...              <Parent post id>"
            }
        ],
        "cursor": "...                      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>POST /post/id/:id/loop</summary>
Mark video as looped and increase its total loop count.
There appears to be no ratelimit to marking posts as looped, so videos can be looped more times
than they could be watched in the same timeframe


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Post looped
Post looped

This post has been marked as looped, and its loop count has been updated

```JSON
{
    "data": {
        "postID": "...      <ID of the looped post>",
        "loopCount": "...   <Updated loop count>"
    },
    "success": 1
}
```

- 200:1101 - Bad request format
Bad request format

The information sent is either malformed, has missing keys, or has unexpected extra keys.
It cannot be used. This should be treated similarly too an HTTP 400 bad request


```JSON
{
    "error": {
        "code": 1101,
        "message": "bad request format"
    },
    "success": 0
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /timeline</summary>
Get posts in the timeline of the authed user

__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Timeline feed slice fetched
Timeline feed slice fetched

A slice of the timeline feed was fetched

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "posts": "[...]     <Array of posts>",
        "cursor": "...      <Pagination cursor>",
        "<->": "            <Only some feeds have cursors, sometimes>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>


<details>
<summary>GET /timeline/rebytes</summary>
Posts that have been rebyted into your timeline.
Essentially post objects wrapped in rebyte info, with the regular id -> user table in feeds


__headers__

|name|value|required|
| - | - | - |
|authorization|The token returned when logging in or creating an account|True|
|user-agent|The user agent of the device using this app|False|

__responses__

- 200 - Feed slice fetched
Feed slice fetched

A slice of posts of this feed were fetched with usermap and pagination data

```JSON
{
    "data": {
        "accounts": "{...}  <id -> user map>",
        "rebytes": "[...]   <Array of post rebytes>",
        "cursor": "...      <Pagination cursor>"
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>
