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

### Conversion Information

This API document aims to standardize the Cointaxes API for external use. The
following specification is what the API **should** become. Here is a summary of
the changes:

* Standardizes on "createdAt" and "updatedAt" for all objects

* Adds an "Exchanges" endpoint so third parties can get a user's exchanges list in a single call

* All endpoints follow REST standards when it comes to when to use GET, POST, PUT, and DELETE HTTP methods

* Objects are always identified by the objects "id" attribute and related objects are identified by "<ObjectType>Id"

* All object attributes are always accessed at the top level, no GETs on a nested route (e.g. /transactions/gifts)

* The user object returns a subset of values when the user is not authenticated

* Index collections are returned in an attribute named "data"

* Keys and Files are top level resources, but always require an exchange

* Exchanges are a real object, and not simply recorded as "location" or "locationName"

* Naming conventions for the same objets are consistent (e.g. not using location and exchangeName)

* Scopes are defined by search parameters (e.g. `/transactions?type=TRADE`) over nested paths

* Payments methods and paths changed to follow REST spec.

* Payment is identified by ID rather then an ID from an outside source (e.g. `"paymentId": "PAY-48L623731R2051135LLA2ZVB"` for PayPal payment)


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
`PATCH /users/65`

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

## Create File

### HTTP Request
`POST /files`

```json
Payload
{
  "exchangeId":1,
  "url":"myfile.csv",
  "kind":"WITHDRAWAL",
}
```

## Update File

### HTTP Request

`PATCH /files/1`

```json
Payload
{
  "status":"FAILED",
}
```

## Delete File

### HTTP Request
`DELETE /files/1`

# Keys

## Get Keys

### HTTP Request
`GET /keys`

```json
Response
{
  "data": [
    {
      "exchangeId":1,
      "publicKey": "data",
      "passphrase": "password123",
      "locationType": "exchange",
      "location": "binance",
      "clientId": "1234abc"  
    },
    {      
      "exchangeId":1,
      "publicKey": "data",
      "passphrase": "password123",
      "locationType": "exchange",
      "location": "binance",
      "clientId": "1234abc"  
    }
  ]
}
```

## Create Key

### HTTP Request
`POST /exchanges/1/keys`

```json
Payload
{
  "publicKey": "data",
  "privateKey": "data",
  "passPhrase": "data",
  "clientId": "1234abc"
}
```

## Update Key

### HTTP Request
`PUT /keys/1`

```json
Payload
{
  "privateKey": "data"
}
```

## Delete Key

### HTTP Request
`DELETE /keys/1`

# Transactions

## Get Transactions

### HTTP Request
`GET /transactions`

```json
Response
{
  "data": [
    {
      "id": 1,
      "exchangeId":1,
      "userId": 453,
      "type": "DEPOSIT",
      "category": "FEE",
      "coin": "USD",
      "coinAmount": 73.41,
      "usdPricePerCoin": 1,
      "usdFee": 0,
      "address": "58e19be779874971e72f159a",
      "manual": false,
      "createdAt": "Apr 3, 2017 1:22:08 AM",
      "updatedAt": "Apr 3, 2017 1:22:08 AM",
    },
    {
      "id": 2,
      "exchangeId":1,
      "userId": 453,
      "type": "DEPOSIT",
      "category": "FEE",
      "coin": "USD",
      "coinAmount": 73.41,
      "usdPricePerCoin": 1,
      "usdFee": 0,
      "address": "58e19be779874971e72f159a",
      "manual": false,
      "createdAt": "Apr 3, 2017 1:22:08 AM",
      "updatedAt": "Apr 3, 2017 1:22:08 AM",
    },
  ]
}
```

## Create Transaction

### HTTP Request
`POST /transactions`

```json
Payload
{
  "exchangeId":1,
  "address":"address",
  "type":"TRADE",
  "category":"TRADE",
  "coin":"BTC",
  "coinAmount":"0.5"
}
```

## Update Transaction

### HTTP Request
`PUT /transactions/1`

```json
Payload
{
  "type": "GIFT"
}
```

## Delete Transaction

### HTTP Request
`DELETE /transactions/1`

# Payments

## Create Payment

### HTTP Request
`POST /payments`

```json
Payload
{
  "productYear": 2017,
  "productType": "TAX_FORM",
  "paymentSource": "STRIPE",
  "promoCode": "freestuff"
}

Response
{
  "id": 28,
  "userId": 158,
  "paymentSourceId": 2,
  "productId": 3,
  "amount": 49.99,
  "tax": 0,
  "currency": "USD",
  "status": "INITIATE"
}
```

## Update Payment

### HTTP Request
`PUT /payments/28`

```json
Payload (Stripe)
{
  "paymentSource": "STRIPE",
  "payerId": "tok_asdfasdf"
}

Payload (Paypal)
{
  "paymentSource": "PAYPAL",
  "payerId": "W4FU77CRLUEYK"
}

Response
{
  "id": 28,
  "userId": 158,
  "paymentSourceId": 2,
  "productId": 3,
  "amount": 49.99,
  "tax": 0,
  "currency": "USD",
  "status": "SUCCESS"
}
```

# Process

## Trigger Process Start

### HTTP Request
`GET /process?userId=<UserId>&taxTreatment=FIFO&outputCurrency=USD`

# Holdings

I don't know what to do about this endpoint. But maybe we don't want to expose it publicly anyway...?

# Forms

Same with this one...?
