<details>
<summary>GET /account/me/</summary>
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
            "id": "                             <account id>",
            "isRegistered": "true               <Is this user registered?>",
            "isChannel": "false                 <Is this user a channel?>",
            "isSuspended": "false               <Is this account suspended?>",
            "isDeactivated": "false             <Did this user deactivate their account?>",
            "registrationDate": "1580272854     <Account creation Unix timestamp>",
            "username": "robotter               <Account username>",
            "backgroundColor": "#000000         <Account background color",
            "foregroundColor": "#CCD6E9         <Account foreground color",
            "followerCount": "0                 <Subscribers of this account>",
            "followingCount": "0                <Subscriptions of this account>",
            "loopCount": "0                     <Total loops played of this account>",
            "loopsConsumedCount": "0            <Total loops played by this account>"
        }
    },
    "success": 1
}
```

- 401 - Unauthorized
Unauthorized

Unauthorized to make request, either because the authorization header is incorrect or missing


</details>
