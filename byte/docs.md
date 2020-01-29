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
