<details>
<summary>POST /account/register/</summary>
Create a profile

```JSON
{
    "service": "google",
    "token": "<google oauth token>",
    "username": "robotter"
}
```

__responses__

- 200 - User registered
User registered

A user was registered and their information was registered

```JSON
{
    "data": {
        "account": {
            "id": "                             <account id>",
            "isRegistered": "true               <Is this user registered?>",
            "isChannel": "false                 <Is this user a channel?>",
            "isSuspended": "false               <Is this account suspended?>",
            "isDeactivated": "false             <Did this user deactivate their account?>",
            "registrationDate": "-62135596800   <Account creation time. Unknown format, appears to be an error>",
            "username": "robotter               <Account username>",
            "backgroundColor": "#000000         <Account background color",
            "foregroundColor": "#CCD6E9         <Account foreground color",
            "followerCount": "0                 <Subscribers of this account>",
            "followingCount": "0                <Subscriptions of this account>",
            "loopCount": "0                     <Total loops played of this account>",
            "loopsConsumedCount": "0            <Total loops played by this account>"
        },
        "token": {
            "token": "                  <auth token>",
            "accountID": "              <account id>",
            "isRegistered": "true       <duplicate>",
            "isDeactivated": "false     <duplicate>"
        }
    },
    "success": 1
}
```

- 200:1300 - OAuth token expired
OAuth token expired

The google oauth token generated for this account create has expired. Likely because you took too long at username select screen

```JSON
{
    "success": 0,
    "error": {
        "code": 1300,
        "message": "invalid Google OAuth Token"
    }
}
```

- 200:1402 - Username taken
Username taken

The username used to sign up is already in use

```JSON
{
    "success": 0,
    "error": {
        "code": 1402,
        "message": "username is already in use"
    }
}
```


</details>


<details>
<summary>POST /account/register/precheck/</summary>
Check username availability. Used when creating an account

__responses__

- 200 - Username free
Username free

The username checked is not in use and can be registered

```JSON
{
    "data": {},
    "success": 1
}
```

- 200:1401 - Username invalid
Username invalid

The username supplied is not valid. This can be because of length, or because of invalid characters like spaces

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

The username checked is in use already

```JSON
{
    "success": 0,
    "error": {
        "code": 1402,
        "message": "username is already in use"
    }
}
```


</details>


<details>
<summary>POST /authenticate/google/</summary>
Post a google token for user authentication. This is for new and existing accounts

__responses__

- 200:1305 - No Such Account
No Such Account

No account exists attached to this google user, and one should be created

```JSON
{
    "success": 0,
    "error": {
        "code": 1305,
        "message": "account not found"
    }
}
```


</details>


<details>
<summary>POST /client/event/</summary>
Likely has to do with event tracking. Appears to always ratelimit me

```JSON
{
    "eventData": {
        "os": "android"
    },
    "eventType": "appOpen"
}
```

__responses__

- 429 - Ratelimited
Ratelimited

The request was not accepted becuase of ratelimiting. Appears to always happen


</details>
