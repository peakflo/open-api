## Getting started

The peakflo APIs allows you to manage your customer, invoice and payment data relevant to your account receivables. All the peakflo APIs uses HTTP methods with JSON request body and responses in general. Authentication can be done using API keys or standard JWT token. This makes it easy to integrate with peakflo. Follow the document to easily get started.


## Security and authentication

The requests made to peakflo API are encrypted. Just use HTTPS in the URL.

You can authenticate using either of the following methods:

### API key authentication

Send the following headers with every request:

- `x-client-id`: Value provided by the Peakflo team
- `x-api-key`: Value managed under **Settings -> Integrations -> API**

### JWT authentication

When authenticating with JWT, a token must be generated and included as a **Bearer** token in the request header.

#### Private key and Access token

As a first step, after creating your peakflo account, peakflo team will provide **Private key** and **Access token**. 
Later use the **Private key** to generate the JWT token which must be sent as part of the Authorization header of your requests.

#### Generating JWT

A JWT token consists of three parts - **header**, **payload** and **signature** with **.** as a separator between these values. Example,

`xxxxx.yyyyy.zzzzz`

#### Header

Header includes the signing algorithm and the type of the token. Use **RS256** as the algorithm and JWT as the type

```json
{
  "typ": "JWT",
  "alg": "RS256"
}
```

#### Payload

Payload includes the claims. Your payload must contain following claims,
   -  iss(issuer)
   -  aud(peakflo)
   -  acc(access token)
   -  sub(subject) 
   -  iat(issued at)
   -  exp(expiration time)


Claim  | Value 
---------|----------
 iss | "peakflo"
 aud | "peakflo"
 acc | Your access token
 sub | Your company Id
 iat | Token issued time. Must be a numeric date
 exp | Token expiry time. Must be a numeric date

Example  
 ```json
{
  "iss": "peakflo",
  "aud": "peakflo",
  "acc": "AIzaSyDrBPSr6lmyBG-iWC_cEW3t67cwO2wdfgR",
  "sub": "mcWinCo",
  "iat": "1475874457",
  "exp": "1475878357"
}
```

#### Signature

The third part of the token which helps in message verification is made up of **encoded header**, **encoded payload **and your **Private key**. Use **RSASHA256** to create the signature in the following way


> RSASHA256(
>   base64UrlEncode(header) + "." +
>   base64UrlEncode(payload),
>   Private key)

Use the resultant token in the **AUTHORIZATION** header of your request as 
**Bearer** token

#### Recommendations
 - Generate your tokens with shorter expiry time.
 - Store your private key and access token in a secure location.
 - Make sure the tokens are not shared publicly
 - Always use HTTPS when making calls to peakflo APIs
 

## Limits

Just like any good API, we control the rate at which you can call peakflo APIs. This is necessary to prevent the overall health and availability of the service and serve all our users in a fair manner. 

API Requests are limited to **100 requests per second** per account



## Important information

### Date format
All dates in peakflo API are strings using UTC and they are in **ISO 8601** format with both date and time

```json
Example: 2021-03-24T18:06:03Z
```

### Currency format

Peakflo API follow **ISO 4217** as the currency format across the services

```json
Example: USD, SGD, INR
```
