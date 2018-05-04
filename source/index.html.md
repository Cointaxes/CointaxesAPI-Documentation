---

title: Cointaxes API

language_tabs:
   - JSON

includes:
   - errors

search: true

---

# Introduction

**Version:** Internal Pre-Alpha

# Users

## Get User

### HTTP Request
`GET /users/65`

`GET /me`

```json
Unauthenticated result
{
  "id":65,
  "email":"testerstesters@hotmail.com",
  "referredBy":null,
  "createDate":null,
  "updateDate":"2018-03-17T14:20:51.000+0000",
  "referrals": []
}

Authenticated result
{
  "id":65,
  "firstName":"Ken",
  "lastName":"Stipek",
  "email":"testerstesters@hotmail.com",
  "userStatusId": 1,
  "storageKey":"JnVx7fTQWILEwRNagEWlvsRTJdzIHJQ7D649rVHo1Z57JCNG7h7GbNniXWgocAlN",
  "timezone":"Pacific Standard Time (Mexico)",
  "referredBy":null,
  "createDate":null,
  "updateDate":"2018-03-17T14:20:51.000+0000",
  "prelaunchWhitelisted":true,
  "coinbaseUser":false,
  "facebookUser":false,
  "googleUser":false,
  "referrals": []
}
```

## Create User

### HTTP Request
`POST /users`

```json
Payload
{
  "email":"testerstesters@hotmail.com",
  "password":"password",
  "timezone":"Pacific Standard Time (Mexico)",
  "referredBy":null
}

Response
{
  "id":65,
  "firstName":"Ken",
  "lastName":"Stipek",
  "email":"testerstesters@hotmail.com",
  "userStatusId": 1,
  "storageKey":"JnVx7fTQWILEwRNagEWlvsRTJdzIHJQ7D649rVHo1Z57JCNG7h7GbNniXWgocAlN",
  "timezone":"Pacific Standard Time (Mexico)",
  "referredBy":null,
  "createDate":null,
  "updateDate":"2018-03-17T14:20:51.000+0000",
  "prelaunchWhitelisted":true,
  "coinbaseUser":false,
  "facebookUser":false,
  "googleUser":false,
  "referrals": []
}
```

## Update User

### HTTP Request
`PUT /users/65`

```json
Payload
{
  "timezone":"Eastern Standard Time (New York)",
}

Response
{
  "userId":65,
  "email":"testerstesters@hotmail.com",
  "userStatusId": 1,
  "currency":"USD",
  "storageKey":"JnVx7fTQWILEwRNagEWlvsRTJdzIHJQ7D649rVHo1Z57JCNG7h7GbNniXWgocAlN",
  "timezone":"Eastern Standard Time (New York)",
  "referredBy":null,
  "createDate":null,
  "updateDate":"2018-03-17T14:20:51.000+0000",
  "prelaunchWhitelisted":true,
  "coinbaseUser":false,
  "facebookUser":false,
  "googleUser":false,
  "referrals": []
}
```

# Exchanges

## Get Exchanges

### HTTP Request
`GET /exchanges`

```json
Response
{
  "data": [
    {
      "id":1,
      "userId": 65,
      "name":"coinbase",
      "createdAt":"2018-03-17T14:20:51.000+0000",
      "updatedAt":"2018-03-17T14:20:51.000+0000"
    },
    {
      "id":2,
      "userId": 65,
      "name":"kraken",
      "createdAt":"2018-03-17T14:20:51.000+0000",
      "updatedAt":"2018-03-17T14:20:51.000+0000"
    },
  ]
}
```

## Get Exchange

### HTTP Request
`GET /exchanges/1`

```json
Response
{
  "id":1,
  "userId": 65,
  "name":"coinbase",
  "createdAt":"2018-03-17T14:20:51.000+0000",
  "updatedAt":"2018-03-17T14:20:51.000+0000"
}
```

## Create Exchange

### HTTP Request
`POST /exchanges`

```json
Payload
{
  "userId": 65,
  "name":"bittrex"
}

Response
{
  "id":3,
  "userId": 65,
  "name":"bittrex",
  "createdAt":"2018-03-17T14:20:51.000+0000",
  "updatedAt":"2018-03-17T14:20:51.000+0000"
}
```

## Delete Exchange

### HTTP Request
`DELETE /exchanges/3`

# Files

## Get Files

### HTTP Request
`GET /files`

`GET /exchanges/1/files`

```json
Response
{
  "data": [
     {
        "id":1,
        "exchangeId":1,
        "url":"myfile.csv",
        "kind":"WITHDRAWAL",
        "status":"INITIAL",
        "createdAt":"2018-03-18T12:49:08.000+0000",
        "updatedAt":"2018-03-18T12:49:08.000+0000"
     },
     {
        "id":2,
        "exchangeId":1,
        "url":"myfile2.csv",
        "kind":"WITHDRAWAL",
        "status":"INITIAL",
        "createdAt":"2018-03-18T12:49:08.000+0000",
        "updatedAt":"2018-03-18T12:49:08.000+0000"
     }
  ]
}
````

# Keys

## Get Key

### HTTP Request
`GET /exchanges/1/keys`
