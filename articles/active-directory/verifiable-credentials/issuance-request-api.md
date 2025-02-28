---
title: Specify the Request Service REST API issuance request (preview)
description: Learn how to issue a verifiable credential that you've issued.
documentationCenter: ''
author: barclayn
manager: rkarlin
ms.service: decentralized-identity
ms.topic: reference
ms.subservice: verifiable-credentials
ms.date: 10/08/2021
ms.author: barclayn

#Customer intent: As an administrator, I am trying to learn the process of revoking verifiable credentials that I have issued.
---

# Request Service REST API issuance specification (preview)

[!INCLUDE [Verifiable Credentials announcement](../../../includes/verifiable-credentials-brand.md)]

Azure Active Directory (Azure AD) Verifiable Credentials includes the Request Service REST API. This API allows you to issue and verify a credential. This article specifies the Request Service REST API for an issuance request.

## HTTP request

The Request Service REST API issuance request supports the following HTTP method:

| Method |Notes  |
|---------|---------|
|POST | With JSON payload as specified in this article. |

The Request Service REST API issuance request requires the following HTTP headers:

| Method |Value  |
|---------|---------|
|`Authorization`| Attach the access token as a bearer token to the authorization header in an HTTP request. For example, `Authorization: Bearer <token>`.|
|`Content-Type`| `Application/json`|

Construct an HTTP POST request to the Request Service REST API. Replace the `{tenantID}` with your tenant ID or tenant name.

```http
https://beta.did.msidentity.com/v1.0/{tenantID}/verifiablecredentials/request
```

The following HTTP request demonstrates a request to the Request Service REST API:

```http
POST https://beta.did.msidentity.com/v1.0/contoso.onmicrosoft.com/verifiablecredentials/request
Content-Type: application/json
Authorization: Bearer  <token>

{
    "includeQRCode": true, 
        "callback": {  
            "url": "https://wwww.contoso.com/vc/callback",  
            "state": "Aaaabbbb11112222", 
            "headers": { 
                "api-key": "an-api-key-can-go-here" 
              }  
        }, 
    ... 
}
```  

The following permission is required to call the Request Service REST API. For more information, see [Grant permissions to get access tokens](verifiable-credentials-configure-tenant.md#grant-permissions-to-get-access-tokens).

| Permission type | Permission  |
|---------|---------|
| Application | bbb94529-53a3-4be5-a069-7eaf2712b826/.default|

## Issuance request payload

The issuance request payload contains information about your verifiable credentials issuance request. The following example demonstrates an issuance request by using a PIN code flow with user claims, such as first name and last name. The result of this request returns a QR code with a link to start the issuance process.

```json
{
    "includeQRCode": true,
    "callback": {
        "url": "https://www.contoso.com/api/issuer/issuanceCallback",
        "state": "de19cb6b-36c1-45fe-9409-909a51292a9c",
        "headers": {
            "api-key": "OPTIONAL API-KEY for VERIFIER CALLBACK API"
        }
    },
    "authority": "did:ion:EiCLL8lzCqlGLYTGbjwgR6SN6OkIjO6uUKyF5zM7fQZ8Jg:eyJkZWx0YSI6eyJwYXRjaGVzIjpbeyJhY3Rpb24iOiJyZXBsYWNlIiwiZG9jdW1lbnQiOnsicHVibGljS2V5cyI6W3siaWQiOiJzaWdfOTAyZmM2NmUiLCJwdWJsaWNLZXlKd2siOnsiY3J2Ijoic2VjcDI1NmsxIiwia3R5IjoiRUMiLCJ4IjoiTEdUOWk3aFYzN1dUcFhHcUg5c1VDek...",
    "registration": {
        "clientName": "Verifiable Credential Expert Sample"
    },
    "issuance": {
        "type": "VerifiedCredentialExpert",
        "manifest": "https://beta.did.msidentity.com/v1.0/12345678-0000-0000-0000-000000000000/verifiableCredential/contracts/VerifiedCredentialExpert",
        "pin": {
            "value": "3539",
            "length": 4
        },
        "claims": {
            "given_name": "Megan",
            "family_name": "Bowen"
        }
    }
}
```

The payload contains the following properties:  

|Parameter |Type  | Description |
|---------|---------|---------|
| `includeQRCode` |  Boolean |   Determines whether a QR code is included in the response of this request. Present the QR code and ask the user to scan it. Scanning the QR code launches the authenticator app with this issuance request. Possible values are `true` (default) or `false`. When you set the value to `false`, use the return `url` property to render a deep link.  |
| `authority` | string|  The issuer's decentralized identifier (DID). For more information, see [Gather credentials and environment details to set up your sample application](verifiable-credentials-configure-issuer.md).|
| `registration` | [RequestRegistration](#requestregistration-type)|  Provides information about the issuer that can be displayed in the authenticator app. |
| `issuance` | [RequestIssuance](#requestissuance-type)| Provides information about the issuance request.  |
|`callback`|  [Callback](#callback-type)| Mandatory. Allows the developer to asynchronously get information on the flow during the verifiable credential issuance process. For example, the developer might want a call when the user has scanned the QR code or if the issuance request succeeds or fails.|

### RequestRegistration type

The `RequestRegistration` type provides information registration for the issuer. The `RequestRegistration` type contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `clientName` | string|  A display name of the issuer of the verifiable credential.  |
| `logoUrl` |  string |  Optional. The URL for the issuer logo.  |
| `termsOfServiceUrl` |  string | Optional. The URL for the terms of use of the verifiable credential that you are issuing.  |

> [!NOTE]
> At this time, the `RequestRegistration` information isn't presented during the issuance in the Microsoft Authenticator app. This information can, however, be used in the payload.

### RequestIssuance type

The `RequestIssuance` type provides information required for verifiable credential issuance. There are currently three input types that you can send in `RequestIssuance`. Azure AD Verifiable Credentials uses these types to insert claims into a verifiable credential, and attest to that information with the issuer's DID. The following are the three types:

- ID token
- Verifiable credentials via a verifiable presentation
- Self-attested claims

You can find detailed information about the input types in [Customizing your verifiable credential](credential-design.md). 

The `RequestIssuance` type contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `type` |  string |  The verifiable credential type. Should match the type as defined in the verifiable credential manifest. For example: `VerifiedCredentialExpert`. For more information, see [Create the verified credential expert card in Azure](verifiable-credentials-configure-issuer.md). |
| `manifest` | string| The URL of the verifiable credential manifest document. For more information, see [Gather credentials and environment details to set up your sample application](verifiable-credentials-configure-issuer.md).|
| `claims` | string| Optional. Include a collection of assertions made about the subject in the verifiable credential. For PIN code flow, it's important that you provide the user's first name and last name. For more information, see [Verifiable credential names](verifiable-credentials-configure-issuer.md#verifiable-credential-names). |
| `pin` | [PIN](#pin-type)| Optional. A PIN number to provide extra security during issuance. For PIN code flow, this property is required. You generate a PIN code, and present it to the user in your app. The user must provide the PIN code that you generated. |

### pin type

The `pin` type defines a PIN code that can be displayed as part of the issuance. `pin` is optional, and, if used, should always be sent out-of-band. When you're using a HASH PIN code, you must define the `salt`, `alg`, and `iterations` properties. `pin` contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `value` | string| Contains the PIN value in plain text. When you're using a hashed PIN, the value property contains the salted hash, base64 encoded.|
| `type` | string|  The type of the PIN code. Possible value: `numeric` (default). |
| `length` | integer|  The length of the PIN code. The default length is 6, the minimum is 4, and the maximum is 16.|
| `salt` | string|  The salt of the hashed PIN code. The salt is prepended during hash computation. Encoding: UTF-8. |
| `alg` | string|  The hashing algorithm for the hashed PIN. Supported algorithm: `sha256`. |
| `iterations` | integer| The number of hashing iterations. Possible value: `1`.|

### Callback type

The Request Service REST API generates several events to the callback endpoint. Those events allow you to update the UI and continue the process after the results are returned to the application. The `Callback` type contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `url` | string| URI to the callback endpoint of your application. The URI must point to a reachable endpoint on the internet otherwise the service will throw callback URL unreadable error. Accepted formats IPv4, IPv6 or DNS resolvable hostname |
| `state` | string| Associates with the state passed in the original payload. |
| `headers` | string| Optional. You can include a collection of HTTP headers required by the receiving end of the POST message. The current supported header values are the `api-key` or the `Authorization` headers. Any other header will throw an invalid callback header error|

## Successful response

If successful, this method returns a response code (*HTTP 201 Created*), and a collection of event objects in the response body. The following JSON demonstrates a successful response:

```json
{  
    "requestId": :"799f23ea-5241-45af-99ad-cf8e5018814e",  
    "url": "openid://vc?request_uri=https://beta.did.msidentity.com/v1.0/12345678-0000-0000-0000-000000000000/verifiablecredentials/request/178319f7-20be-4945-80fb-7d52d47ae82e",  
    "expiry": 1622227690,  
    "qrCode": "data:image/png;base64,iVBORw0KggoA<SNIP>"  
} 
```

The response contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `requestId`| string | An autogenerated correlation ID. The [callback](#callback-events) uses the same request, allowing you to keep track of the issuance request and its callbacks. |
| `url`|  string| A URL that launches the authenticator app and starts the issuance process. You can present this URL to the user if they can't scan the QR code. |
| `expiry`| integer| Indicates when the response will expire. |
| `qrCode`| string | A QR code that user can scan to start the issuance flow. |

When your app receives the response, the app needs to present the QR code to the user. The user scans the QR code, which opens the authenticator app and starts the issuance process.

## Error response

Error responses also can be returned so that the app can handle them appropriately. The following JSON shows an unauthorized error message:


```json
{
    "requestId": "d60b068e7fbd975896e179b99347866a",
    "date": "Wed, 29 Sep 2021 21:49:00 GMT",
    "error": {
        "code": "unauthorized",
        "message": "Failed to authenticate the request."
    }
}
```

The response contains the following properties:

|Property |Type |Description |
|---------|---------|---------|
| `requestId`| string | An autogenerated request ID.|
| `date`| date| The time of the error. |
| `error.code` | string| The return error code. |
| `error.message`| string| The error message. |

## Callback events

The callback endpoint is called when a user scans the QR code, uses the deep link the authenticator app, or finishes the issuance process. 

|Property |Type |Description |
|---------|---------|---------|
| `requestId`| string | Mapped to the original request when the payload was posted to the Verifiable Credentials service.|
| `code` |string |The code returned when the request has an error. Possible values: <ul><li>`request_retrieved`: The user scanned the QR code or selected the link that starts the issuance flow.</li><li>`issuance_successful`: The issuance of the verifiable credentials was successful.</li><li>`Issuance_error`: There was an error during issuance. For details, see the `error` property.</li></ul>    |
| `state` |string| Returns the state value that you passed in the original payload.   |
| `error`| error | When the `code` property value is `Issuance_error`, this property contains information about the error.| 
| `error.code` | string| The return error code. |
| `error.message`| string| The error message. |

The following example demonstrates a callback payload when the authenticator app starts the issuance request:

```json
{  
    "requestId":"aef2133ba45886ce2c38974339ba1057",  
    "code":"request_retrieved",  
    "state":"Wy0ThUz1gSasAjS1"
} 
```

The following example demonstrates a callback payload after the user successfully completes the issuance process:

```json
{  
    "requestId":"87e1cb24-9096-409f-81cb-9e645f23a4ba",
    "code":"issuance_successful",
    "state":"f3d94e35-ca5f-4b1b-a7d7-a88caa05e322",
} 
```

### Callback errors  

The callback endpoint might be called with an error message. The following table lists the error codes:

|Message  |Definition    |
|---------|---------|
| `fetch_contract_error*`| Unable to fetch the verifiable credential contract. This error usually happens when the API can't fetch the manifest you specify in the request payload [RequestIssuance object](#requestissuance-type).|
| `issuance_service_error*` | The Verifiable Credentials service isn't able to validate requirements, or something went wrong in Verifiable Credentials.|
| `unspecified_error`| This error is uncommon, but worth investigating. |

The following example demonstrates a callback payload when an error occurred:

```json
{  
    "requestId":"87e1cb24-9096-409f-81cb-9e645f23a4ba",  
    "code": "issuance_error",  
    "state":"f3d94e35-ca5f-4b1b-a7d7-a88caa05e322",  
    "error": { 
      "code":"IssuanceFlowFailed", 
      "message":"issuance_service_error”, 
    } 
} 
``` 

## Next steps

Learn [how to call the Request Service REST API](get-started-request-api.md).
